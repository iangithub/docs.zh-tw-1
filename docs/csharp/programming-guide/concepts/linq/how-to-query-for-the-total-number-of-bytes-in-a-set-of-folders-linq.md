---
title: 作法：查詢一組資料夾中的位元組總數 (LINQ) (C#)
ms.date: 07/20/2015
ms.assetid: a01bd1d4-133c-4ca2-aa4e-e93e81d6076c
ms.openlocfilehash: 04eed82041dc3c0818b0205f5198abe6e9eb228e
ms.sourcegitcommit: c7a7e1468bf0fa7f7065de951d60dfc8d5ba89f5
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/14/2019
ms.locfileid: "65585686"
---
# <a name="how-to-query-for-the-total-number-of-bytes-in-a-set-of-folders-linq-c"></a>作法：查詢一組資料夾中的位元組總數 (LINQ) (C#)
此範例示範如何擷取所指定資料夾及其所有子資料夾中之所有檔案使用的位元組總數。  
  
## <a name="example"></a>範例  
 <xref:System.Linq.Enumerable.Sum%2A> 方法會新增 `select` 子句中選取之所有項目的值。 您可以輕鬆地修改此查詢以擷取指定目錄樹狀結構中的最大或最小檔案，方法是呼叫 <xref:System.Linq.Enumerable.Min%2A> 或 <xref:System.Linq.Enumerable.Max%2A> 方法，而非 <xref:System.Linq.Enumerable.Sum%2A>。  
  
```csharp  
class QuerySize  
{  
    public static void Main()  
    {  
        string startFolder = @"c:\program files\Microsoft Visual Studio 9.0\VC#";  
  
        // Take a snapshot of the file system.  
        // This method assumes that the application has discovery permissions  
        // for all folders under the specified path.  
        IEnumerable<string> fileList = System.IO.Directory.GetFiles(startFolder, "*.*", System.IO.SearchOption.AllDirectories);  
  
        var fileQuery = from file in fileList  
                        select GetFileLength(file);  
  
        // Cache the results to avoid multiple trips to the file system.  
        long[] fileLengths = fileQuery.ToArray();  
  
        // Return the size of the largest file  
        long largestFile = fileLengths.Max();  
  
        // Return the total number of bytes in all the files under the specified folder.  
        long totalBytes = fileLengths.Sum();  
  
        Console.WriteLine("There are {0} bytes in {1} files under {2}",  
            totalBytes, fileList.Count(), startFolder);  
        Console.WriteLine("The largest files is {0} bytes.", largestFile);  
  
        // Keep the console window open in debug mode.  
        Console.WriteLine("Press any key to exit.");  
        Console.ReadKey();  
    }  
  
    // This method is used to swallow the possible exception  
    // that can be raised when accessing the System.IO.FileInfo.Length property.  
    static long GetFileLength(string filename)  
    {  
        long retval;  
        try  
        {  
            System.IO.FileInfo fi = new System.IO.FileInfo(filename);  
            retval = fi.Length;  
        }  
        catch (System.IO.FileNotFoundException)  
        {  
            // If a file is no longer present,  
            // just add zero bytes to the total.  
            retval = 0;  
        }  
        return retval;  
    }  
}  
```  
  
 如果您只需要計算所指定樹狀目錄中的位元組數，則可以用更有效率的方式進行這項作業，而不需要建立 LINQ 查詢，原因是這種查詢需要多花時間來建立清單集合作為資料來源。 當查詢越複雜，或需要對相同資料來源執行多個查詢時，LINQ 方式就越有用。  
  
 查詢會呼叫外面另一個方法來取得檔案長度。 這麼做是要解決可能會因下列狀況引發的例外狀況：自呼叫 `GetFiles` 而建立 <xref:System.IO.FileInfo> 物件後，有另一個執行緒刪除了檔案。 即使已建立 <xref:System.IO.FileInfo> 物件，還是可能會發生這個例外狀況，原因是 <xref:System.IO.FileInfo> 物件會在它的 <xref:System.IO.FileInfo.Length%2A> 屬性第一次受到存取時，嘗試用目前最新的長度來重新整理這個屬性。 讓這個作業進入查詢外部的 try-catch 區塊，程式碼就會遵循規則，以避免查詢中會造成副作業的作業。 一般而言，處理例外狀況時需要十分小心，以確定應用程式不是處於未知狀態。  
  
## <a name="compiling-the-code"></a>編譯程式碼  
建立 C# 主控台應用程式專案，以及具有 `using` 指示詞的 System.Linq 和 System.IO 命名空間。
  
## <a name="see-also"></a>另請參閱

- [LINQ to Objects (C#)](../../../../csharp/programming-guide/concepts/linq/linq-to-objects.md)
- [LINQ 和檔案目錄 (C#)](../../../../csharp/programming-guide/concepts/linq/linq-and-file-directories.md)
