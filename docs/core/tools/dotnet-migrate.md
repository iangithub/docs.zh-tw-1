---
title: dotnet migrate 命令
description: dotnet migrate 命令會移轉專案及其所有相依性。
ms.date: 06/26/2019
ms.openlocfilehash: 3304f666d15d9188cdae76a401747d91791f817f
ms.sourcegitcommit: b5c59eaaf8bf48ef3ec259f228cb328d6d4c0ceb
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/03/2019
ms.locfileid: "67539391"
---
# <a name="dotnet-migrate"></a>dotnet migrate

**本主題適用於：✓** .NET Core 1.x SDK 和更新版本

<!-- todo: uncomment when all CLI commands are reviewed
[!INCLUDE [topic-appliesto-net-core-all](../../../includes/topic-appliesto-net-core-all.md)]
-->

## <a name="name"></a>名稱

`dotnet migrate` - 將 Preview 2 .NET Core 專案移轉至 .NET Core SDK 型專案。

> [!NOTE]
> 在下一個預覽版本中，`dotnet migrate` 會從 .NET Core 3.0 SDK 中移除。

## <a name="synopsis"></a>概要

```
dotnet migrate [<SOLUTION_FILE|PROJECT_DIR>] [--format-report-file-json] [-r|--report-file] [-s|--skip-project-references] [--skip-backup] [-t|--template-file] [-v|--sdk-package-version] [-x|--xproj-file]
dotnet migrate [-h|--help]
```

## <a name="description"></a>說明

`dotnet migrate` 命令會將有效的 Preview 2 *project.json* 型專案移轉至有效的 .NET Core SDK 型 *csproj* 專案。

根據預設，命令會移轉根專案和根專案包含的任何專案參考。 可以在執行階段使用 `--skip-project-references` 選項停用此行為。

可針對下列資產進行移轉：

* 指定要移轉之 *project.json* 檔案的單一專案。
* 於 *global.json* 檔案中指定的所有目錄，方法是傳遞 *global.json* 檔案的路徑。
* *solution.sln* 檔案，移轉方案參考的專案。
* 指定之目錄的所有子目錄，以遞迴方式進行。

`dotnet migrate` 命令會在 `backup` 目錄 (若目錄不存在則會建立) 中保留移轉的 *project.json* 檔案。 使用 `--skip-backup` 選項會覆寫此行為。

根據預設，移轉作業會將移轉程序的狀態輸出到標準輸出 (STDOUT)。 如果使用 `--report-file <REPORT_FILE>` 選項，則輸出會儲存到指定的檔案。

`dotnet migrate` 命令只支援有效的 Preview 2 *project.json* 型專案。 這表示您無法使用它將 DNX 或 Preview 1 *project.json* 型專案直接移轉到 MSBuild/csproj 專案。 您必須先手動將專案移轉到 Preview 2 *project.json* 型專案，然後再使用 `dotnet migrate` 命令移轉該專案。

## <a name="arguments"></a>引數

`PROJECT_JSON/GLOBAL_JSON/SOLUTION_FILE/PROJECT_DIR`

下列其中一項的路徑：

* 要移轉的 *project.json* 檔案。
* *global.json* 檔案：會移轉 *global.json* 中指定的資料夾。
* *solution.sln* 檔案：會移轉方案參考的專案。
* 要移轉的目錄：會在指定目錄內遞迴地搜尋要移轉的 *project.json* 檔案。

如果未指定，則預設值是目前的目錄。

## <a name="options"></a>選項

`--format-report-file-json <REPORT_FILE>`

將移轉報告檔案輸出為 JSON，而非使用者訊息。

`-h|--help`

印出命令的簡短說明。

`-r|--report-file <REPORT_FILE>`

除了主控台外，也將移轉報告輸出到檔案。

`-s|--skip-project-references [Debug|Release]`

略過移轉專案參考。 根據預設，專案參考是以遞迴方式移轉。

`--skip-backup`

成功移轉後，略過將 *project.json*、*global.json* 和 *\*.xproj* 移動至 `backup` 目錄。

`-t|--template-file <TEMPLATE_FILE>`

要用於移轉的範本 csproj 檔案。 根據預設，會使用 `dotnet new console` 所置放的相同範本。

`-v|--sdk-package-version <VERSION>`

在已移轉之應用程式中參考的 SDK 套件版本。 預設為 `dotnet new` 中的 SDK 版本。

`-x|--xproj-file <FILE>`

要使用之 xproj 檔案的路徑。 當專案目錄中有多個 xproj 時為必要。

## <a name="examples"></a>範例

移轉目前目錄中的專案和所有其專案對專案相依性：

`dotnet migrate`

移轉 *global.json* 檔案包含的所有專案：

`dotnet migrate path/to/global.json`

只移轉目前的專案而不移轉專案對專案 (P2P) 相依性。 此外，使用特定的 SDK 版本：

`dotnet migrate -s -v 1.0.0-preview4`
