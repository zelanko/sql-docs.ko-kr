---
title: ReadOnly 및 ReadWrite 모드 간 Analysis Services 데이터베이스 전환 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- ReadOnly property
- ReadWriteMode command
- operations [Analysis Services - multidimensional data]
ms.assetid: 4eff8181-08dd-4fad-b091-d400fc21a020
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 48bb00cba9a01029da31146f9e98e2ef8b3627d6
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62741365"
---
# <a name="switch-an-analysis-services-database-between-readonly-and-readwrite-modes"></a>ReadOnly 모드와 ReadWrite 모드 간 Analysis Services 데이터베이스 전환
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] DBA(데이터베이스 관리자)가 테이블 형식 또는 다차원 데이터베이스의 읽기/쓰기 모드를 변경해야 하는 경우가 종종 있습니다. 대개 사용자 경험 개선을 위해 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 서버의 풀에서 데이터베이스를 공유하는 것과 같은 비즈니스 요구 사항에 따라 데이터베이스의 읽기/쓰기 모드를 변경합니다.  
  
 데이터베이스 모드는 여러 가지 방법으로 전환할 수 있습니다. 이 문서에서는 다음과 같은 일반적인 시나리오에 대해 설명합니다.  
  
-   대화식으로 다음을 사용 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]  
  
-   AMO를 사용하여 프로그래밍 방식으로 전환  
  
-   XMLA를 사용하여 스크립트로 전환  
  
## <a name="procedures"></a>절차  
  
#### <a name="to-switch-the-readwrite-mode-of-a-database-interactively-using-management-studio"></a>Management Studio를 사용하여 데이터베이스의 읽기/쓰기 모드를 대화식으로 전환하려면  
  
1.  [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]의 왼쪽 또는 오른쪽 창에서 전환할 데이터베이스를 찾습니다.  
  
2.  데이터베이스를 마우스 오른쪽 단추로 누르고 **속성**합니다. 데이터베이스 폴더를 찾은 후 위치를 확인합니다. 빈 데이터베이스 스토리지 위치는 데이터베이스 폴더가 서버 데이터 폴더에 있음을 나타냅니다.  
  
    > [!IMPORTANT]  
    >  데이터베이스를 분리하면 즉시 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]를 사용하여 데이터베이스 위치를 찾을 수 없게 됩니다.  
  
3.  데이터베이스를 마우스 오른쪽 단추로 클릭 하 고 선택 **분리 하는 중...**  
  
4.  분리되는 데이터베이스에 암호를 할당한 후 **확인** 을 클릭하여 분리 명령을 실행합니다.  
  
5.  찾을 합니다 **데이터베이스** 의 왼쪽 또는 오른쪽 창에서 폴더 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]합니다.  
  
6.  마우스 오른쪽 단추로 클릭 합니다 **데이터베이스** 선택한 폴더 **연결 하는 중...**  
  
7.  **폴더** 입력란에 데이터베이스 폴더의 원래 위치를 입력합니다. 또는 찾아보기 단추를 사용할 수 있습니다 (**...** ) 데이터베이스 폴더를 찾습니다.  
  
8.  데이터베이스의 읽기/쓰기 모드를 선택합니다.  
  
9. 3 단계에서 사용 된 암호를 입력 하 고 클릭 **확인** attach 명령을 실행 합니다.  
  
#### <a name="to-switch-the-readwrite-mode-to-a-database-programmatically-using-amo"></a>AMO를 사용하여 데이터베이스의 읽기/쓰기 모드를 프로그래밍 방식으로 전환하려면  
  
1.  C# 애플리케이션에 다음 예제 코드를 적용하고 표시되는 태스크를 완료합니다.  
  
 `private void SwitchReadWrite(Server server, string dbName,`  
  
 `ReadWriteMode dbReadWriteMode)`  
  
 `{`  
  
 `if (server.Databases.ContainsName(dbName))`  
  
 `{`  
  
 `Database db;`  
  
 `string databaseLocation;`  
  
 `db = server.Databases[dbName];`  
  
 `databaseLocation = db.DbStorageLocation;`  
  
 `if (databaseLocation == null)`  
  
 `{`  
  
 `string dataDir = server.ServerProperties["DataDir"].Value;`  
  
 `String[] possibleFolders = Directory.GetDirectories(dataDir, string.Concat(dbName,"*"), SearchOption.TopDirectoryOnly);`  
  
 `if (possibleFolders.Length > 1)`  
  
 `{`  
  
 `List<String> sortedFolders = new List<string>(possibleFolders.Length);`  
  
 `sortedFolders.AddRange(possibleFolders);`  
  
 `sortedFolders.Sort();`  
  
 `databaseLocation = sortedFolders[sortedFolders.Count - 1];`  
  
 `}`  
  
 `else`  
  
 `{`  
  
 `databaseLocation = possibleFolders[0];`  
  
 `}`  
  
 `}`  
  
 `db.Detach();`  
  
 `server.Attach(databaseLocation, dbReadWriteMode);`  
  
 `}`  
  
 `}`  
  
1.  C# 애플리케이션에서 필요한 매개 변수를 사용하여 `SwitchReadWrite()` 를 호출합니다.  
  
2.  코드를 컴파일하고 실행하여 데이터베이스를 이동합니다.  
  
#### <a name="to-switch-the-readwrite-mode-to-a-database-by-script-using-xmla"></a>XMLA를 사용하여 스크립트로 데이터베이스의 읽기/쓰기 모드를 전환하려면  
  
1.  [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]의 왼쪽 또는 오른쪽 창에서 전환할 데이터베이스를 찾습니다.  
  
2.  데이터베이스를 마우스 오른쪽 단추로 누르고 **속성**합니다. 데이터베이스 폴더를 찾은 후 위치를 확인합니다. 빈 데이터베이스 스토리지 위치는 데이터베이스 폴더가 서버 데이터 폴더에 있음을 나타냅니다.  
  
    > [!IMPORTANT]  
    >  데이터베이스를 분리하면 즉시 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]를 사용하여 데이터베이스 위치를 찾을 수 없게 됩니다.  
  
3.  [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]에서 새 XMLA 탭을 엽니다.  
  
4.  다음 XMLA 스크립트 템플릿을 복사합니다.  
  
 `<Detach xmlns="https://schemas.microsoft.com/analysisservices/2003/engine">`  
  
 `<Object>`  
  
 `<DatabaseID>%dbName%</DatabaseID>`  
  
 `<Password>%password%</Password>`  
  
 `</Object>`  
  
 `</Detach>`  
  
1.  `%dbName%` 은 데이터베이스 이름으로 대체하고 `%password%` 는 암호로 대체합니다. % 문자는 템플릿의 일부이므로 제거해야 합니다.  
  
2.  XMLA 명령을 실행합니다.  
  
3.  다음 XMLA 스크립트 템플릿을 새 XMLA 탭에 복사합니다.  
  
 `<Attach xmlns="https://schemas.microsoft.com/analysisservices/2003` `/engine` `">`  
  
 `<Folder>%dbFolder%</Folder>`  
  
 `<ReadWriteMode xmlns="https://schemas.microsoft.com/analysisservices/2008/engine/100">%ReadOnlyMode%</ReadWriteMode>`  
  
 `</Attach>`  
  
1.  `%dbFolder%`는 데이터베이스 폴더의 전체 UNC 경로로 대체하고 `%ReadOnlyMode%`는 해당 값(`ReadOnly` 또는 `ReadWrite`)으로, `%password%`는 암호로 대체합니다. % 문자는 템플릿의 일부이므로 제거해야 합니다.  
  
2.  XMLA 명령을 실행합니다.  
  
## <a name="see-also"></a>관련 항목  
 <xref:Microsoft.AnalysisServices.Server.Attach%2A>   
 <xref:Microsoft.AnalysisServices.Database.Detach%2A>   
 [Analysis Services 데이터베이스 연결 및 분리](attach-and-detach-analysis-services-databases.md)   
 [데이터베이스 저장소 위치](database-storage-location.md)   
 [ReadWriteMode 데이터베이스](database-readwritemodes.md)   
 [Attach 요소](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/attach-element)   
 [Detach 요소](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/detach-element)   
 [ReadWriteMode 요소](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/readwritemode-element)   
 [DbStorageLocation 요소](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/dbstoragelocation-element)  
  
  
