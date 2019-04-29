---
title: Analysis Services 데이터베이스 이동 | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 3247bf2ca459f013131b21a25278bcc6e5d10b9a
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62930898"
---
# <a name="move-an-analysis-services-database"></a>Analysis Services 데이터베이스 이동
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] DBA(데이터베이스 관리자)가 다차원 또는 테이블 형식 model 데이터베이스를 다른 위치로 이동해야 하는 경우가 종종 있습니다. 이러한 경우는 보다 나은 성능, 데이터베이스 확장에 따른 공간 확보, 또는 제품 업그레이드를 위해 데이터베이스를 다른 디스크로 이동하는 것과 같이 대부분 비즈니스 요구 사항에 의해 발생합니다.  
  
 데이터베이스는 여러 가지 방법으로 이동할 수 있습니다. 이 문서에서는 다음과 같은 일반적인 시나리오에 대해 설명합니다.  
  
-   SSMS를 사용하여 대화식으로 이동  
  
-   AMO를 사용하여 프로그래밍 방식으로 이동  
  
-   XMLA를 사용하여 스크립트로 이동  
  
 모든 시나리오에서 사용자는 데이터베이스 폴더에 액세스해야 하고 파일을 원하는 최종 대상으로 이동하기 위한 방법을 사용해야 합니다.  
  
> [!NOTE]  
>  암호를 할당하지 않고 데이터베이스를 분리하면 데이터베이스가 안전하지 않은 상태에 놓이게 됩니다. 데이터베이스에 암호를 할당하여 기밀 정보를 보호하는 것이 좋습니다. 또한 데이터베이스 폴더, 하위 폴더 및 파일에 각각 해당 액세스 보안을 적용하여 무단 액세스를 방지해야 합니다.  
  
## <a name="procedures"></a>절차  
  
#### <a name="moving-a-database-interactively-using-ssms"></a>SSMS를 사용하여 대화식으로 데이터베이스 이동  
  
1.  SSMS의 왼쪽 또는 오른쪽 창에서 이동할 데이터베이스를 찾습니다.  
  
2.  선택한 데이터베이스를 마우스 오른쪽 단추로 클릭 **분리 하는 중...**  
  
3.  분리되는 데이터베이스에 암호를 할당한 후 **확인** 을 클릭하여 분리 명령을 실행합니다.  
  
4.  운영 체제 메커니즘을 사용하거나 파일 이동을 위한 각자의 표준 방법을 사용하여 데이터베이스 폴더를 새 위치로 이동합니다.  
  
5.  SSMS의 왼쪽 또는 오른쪽 창에서 **데이터베이스** 폴더를 찾습니다.  
  
6.  마우스 오른쪽 단추로 클릭 합니다 **데이터베이스** 선택한 폴더 **연결 하는 중...**  
  
7.  **폴더** 입력란에 데이터베이스 폴더의 새 위치를 입력합니다. 또는 찾아보기 단추를 사용할 수 있습니다 (**...** ) 데이터베이스 폴더를 찾습니다.  
  
8.  데이터베이스에 대해 **ReadWrite** 모드를 선택합니다.  
  
9. 3단계에 사용한 암호를 입력하고 **확인** 을 클릭하여 연결 명령을 실행합니다.  
  
#### <a name="moving-a-database-programmatically-using-amo"></a>AMO를 사용하여 프로그래밍 방식으로 데이터베이스 이동  
  
1.  C# 애플리케이션에 다음 예제 코드를 적용하고 표시되는 태스크를 완료합니다.  
  
 `private void MoveDb(Server server, string dbName,`  
  
 `string dbInitialLocation, string dbFinalLocation,`  
  
 `string dbPassword, ReadWriteMode dbReadWriteMode)`  
  
 `{`  
  
 `//Verify dbInitialLocation exists before continuing`  
  
 `if (server.Databases.ContainsName(dbName))`  
  
 `{`  
  
 `Database db;`  
  
 `//Save current cursor and change cursor to Cursors.WaitCursor`  
  
 `db = server.Databases[dbName];`  
  
 `db.Detach(dbPassword);`  
  
 `//Add your own code to copy the database files to the destination where you intend to attach the database`  
  
 `//Verify dbFinalLocation exists before continuing`  
  
 `server.Attach(dbFinalLocation, dbReadWriteMode, dbPassword);`  
  
 `//Restore cursor to its original`  
  
 `}`  
  
 `}`  
  
1.  C# 애플리케이션에서 필요한 매개 변수를 사용하여 `MoveDb()` 를 호출합니다.  
  
2.  코드를 컴파일하고 실행하여 데이터베이스를 이동합니다.  
  
#### <a name="moving-a-database-by-script-using-xmla"></a>XMLA를 사용하여 스크립트로 데이터베이스 이동  
  
1.  SSMS에서 새 XMLA 탭을 엽니다.  
  
2.  다음 XMLA 스크립트 템플릿을 복사합니다.  
  
 `<Detach xmlns="http://schemas.microsoft.com/analysisservices/2003/engine">`  
  
 `<Object>`  
  
 `<DatabaseID>%dbName%</DatabaseID>`  
  
 `<Password>%password%</Password>`  
  
 `</Object>`  
  
 `</Detach>`  
  
1.  `%dbName%` 은 데이터베이스 이름으로 대체하고 `%password%` 는 암호로 대체합니다. % 문자는 템플릿의 일부이므로 제거해야 합니다.  
  
2.  XMLA 명령을 실행합니다.  
  
3.  운영 체제 메커니즘을 사용하거나 파일 이동을 위한 각자의 표준 방법을 사용하여 데이터베이스 폴더를 새 위치로 이동합니다.  
  
4.  다음 XMLA 스크립트 템플릿을 새 XMLA 탭에 복사합니다.  
  
 `<Attach xmlns="http://schemas.microsoft.com/analysisservices/2003/engine">`  
  
 `<Folder>%dbFolder%</Folder>`  
  
 `<ReadWriteMode xmlns="http://schemas.microsoft.com/analysisservices/2008/engine/100">%ReadOnlyMode%</ReadWriteMode>`  
  
 `</Attach>`  
  
1.  `%dbFolder%` 는 데이터베이스 폴더의 전체 UNC 경로로 대체하고 `%ReadOnlyMode%` 는 해당 값( **ReadOnly** 또는 **ReadWrite**)으로, `%password%` 는 암호로 대체합니다. % 문자는 템플릿의 일부이므로 제거해야 합니다.  
  
2.  XMLA 명령을 실행합니다.  
  
## <a name="see-also"></a>관련 항목  
 <xref:Microsoft.AnalysisServices.Core.Server.Attach%2A>   
 <xref:Microsoft.AnalysisServices.Database.Detach%2A>   
 [Analysis Services 데이터베이스 연결 및 분리](../../analysis-services/multidimensional-models/attach-and-detach-analysis-services-databases.md)   
 [데이터베이스 저장소 위치](../../analysis-services/multidimensional-models/database-storage-location.md)   
 [ReadWriteMode 데이터베이스](../../analysis-services/multidimensional-models/database-readwritemodes.md)   
 [Attach 요소](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/attach-element)   
 [Detach 요소](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/detach-element)   
 [ReadWriteMode 요소](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/readwritemode-element)   
 [DbStorageLocation 요소](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/dbstoragelocation-element)  
  
  
