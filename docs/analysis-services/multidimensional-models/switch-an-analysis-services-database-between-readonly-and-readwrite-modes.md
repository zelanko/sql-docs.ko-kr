---
title: ReadOnly 및 ReadWrite 모드 간 Analysis Services 데이터베이스 전환 | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: c6ede109d13c21686400c0f9ce99c22f1118eda9
ms.sourcegitcommit: 7fe14c61083684dc576d88377e32e2fc315b7107
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/26/2018
ms.locfileid: "50147918"
---
# <a name="switch-an-analysis-services-database-between-readonly-and-readwrite-modes"></a>ReadOnly 모드와 ReadWrite 모드 간 Analysis Services 데이터베이스 전환
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스 관리자는 쿼리 작업을 여러 전용 서버에 배포하는 큰 노력의 일환으로 테이블 형식 또는 다차원 데이터베이스의 읽기/쓰기 모드를 변경할 수 있습니다.  
  
 데이터베이스 모드는 여러 가지 방법으로 전환할 수 있습니다. 이 문서에서는 다음과 같은 일반적인 시나리오에 대해 설명합니다.  
  
-   대화식으로 다음을 사용 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]  
  
-   AMO를 사용하여 프로그래밍 방식으로 이동  
  
-   XMLA 또는 TMSL을 사용하여 스크립트로 이동  
  
## <a name="switch-the-readwrite-mode-of-a-database-interactively-using-management-studio"></a>Management Studio를 사용하여 데이터베이스의 읽기/쓰기 모드를 대화식으로 전환  
  
1.  개체 탐색기에서 데이터베이스를 마우스 오른쪽 단추로 클릭하고 **속성**을 선택합니다.  
  
     위치를 확인합니다. 빈 데이터베이스 저장소 위치는 데이터베이스 폴더가 서버 데이터 폴더에 있음을 나타냅니다.  
  
2.  데이터베이스를 마우스 오른쪽 단추로 클릭한 다음 **분리...** 를 선택합니다.  
  
3.  분리되는 데이터베이스에 암호를 할당한 후 **확인** 을 클릭하여 분리 명령을 실행합니다.  
  
4.  개체 탐색기에서 **데이터베이스** 폴더를 마우스 오른쪽 단추로 클릭하고 **연결...** 을 선택합니다.  
  
5.  **폴더** 입력란에 데이터베이스 폴더의 원래 위치를 입력합니다. 또는 찾아보기 단추 (**…**)를 사용하여 데이터베이스 폴더를 찾을 수 있습니다.  
  
6.  데이터베이스의 읽기/쓰기 모드를 선택합니다.  
  
7.  암호를 입력하고 **확인** 을 클릭하여 연결 명령을 실행합니다.  
  
## <a name="switch-the-readwrite-mode-to-a-database-programmatically-using-amo"></a>AMO를 사용하여 데이터베이스의 읽기/쓰기 모드를 프로그래밍 방식으로 전환  
 C# 애플리케이션에서 필요한 매개 변수를 사용하여 `SwitchReadWrite()` 를 호출합니다. 코드를 컴파일하고 실행하여 데이터베이스를 이동합니다.  
  
```  
private void SwitchReadWrite(Server server, string dbName, ReadWriteMode dbReadWriteMode)  
{  
    if (server.Databases.ContainsName(dbName))  
    {  
        Database db;  
        string databaseLocation;  
        db = server.Databases[dbName];  
        databaseLocation = db.DbStorageLocation;  
  
              if (databaseLocation == null)  
            {  
                 string dataDir = server.ServerProperties["DataDir"].Value;  
                 string dataDir = server.ServerProperties["DataDir"].Value;  
                 string dataDir = server.ServerProperties["DataDir"].Value;  
  
    String[] possibleFolders = Directory.GetDirectories(dataDir, string.Concat(dbName,"*"), SearchOption.TopDirectoryOnly);  
  
   if (possibleFolders.Length > 1)  
         {  
         List<String> sortedFolders = new List<string>(possibleFolders.Length);  
         sortedFolders.AddRange(possibleFolders);  
         sortedFolders.Sort();  
         databaseLocation = sortedFolders[sortedFolders.Count - 1];  
         }  
         else  
         {  
         databaseLocation = possibleFolders[0];  
          }  
        }  
    db.Detach();  
    server.Attach(databaseLocation, dbReadWriteMode);  
    }  
}  
  
```  
  
## <a name="switch-the-readwrite-mode-to-a-database-by-script-using-xmla"></a>XMLA를 사용하여 스크립트로 데이터베이스의 읽기/쓰기 모드를 전환  
 다음 지침은 1050, 1100 또는 1103 호환성 모드에서 다차원 데이터베이스 및 테이블 형식 데이터베이스에 적용됩니다.  
  
1.  개체 탐색기에서 데이터베이스를 마우스 오른쪽 단추로 클릭하고 **속성**을 선택합니다.  
  
     위치를 확인합니다. 빈 데이터베이스 저장소 위치는 데이터베이스 폴더가 서버 데이터 폴더에 있음을 나타냅니다.  
  
2.  데이터베이스를 마우스 오른쪽 단추로 클릭한 다음 **분리...** 를 선택합니다.  
  
3.  [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]에서 새 XMLA 탭을 엽니다.  
  
4.  다음 XMLA 스크립트 템플릿을 복사합니다.  
  
    ```  
    <Detach xmlns="http://schemas.microsoft.com/analysisservices/2003/engine">  
       <Object>  
          <DatabaseID>%dbName%</DatabaseID>  
          <Password>%password%</Password>  
       </Object>  
    </Detach>  
    ```  
  
5.  `%dbName%` 은 데이터베이스 이름으로 대체하고 `%password%` 는 암호로 대체합니다. % 문자는 템플릿의 일부이므로 제거해야 합니다.  
  
6.  XMLA 명령을 실행합니다.  
  
7.  다음 XMLA 스크립트 템플릿을 새 XMLA 탭에 복사합니다.  
  
    ```  
    <Attach xmlns="http://schemas.microsoft.com/analysisservices/2003/engine">  
       <Folder>%dbFolder%</Folder>  
       <ReadWriteMode xmlns="http://schemas.microsoft.com/analysisservices/2008/engine/100">%ReadOnlyMode%</ReadWriteMode>  
    </Attach>  
    ```  
  
8.  `%dbFolder%` 는 데이터베이스 폴더의 전체 UNC 경로로 대체하고 `%ReadOnlyMode%` 는 해당 값( **ReadOnly** 또는 **ReadWrite**)으로, `%password%` 는 암호로 대체합니다. % 문자는 템플릿의 일부이므로 제거해야 합니다.  
  
9. XMLA 명령을 실행합니다.  
  
## <a name="see-also"></a>관련 항목  
 <xref:Microsoft.AnalysisServices.Database.Detach%2A>   
 [Analysis Services의 고가용성 및 확장성](../../analysis-services/instances/high-availability-and-scalability-in-analysis-services.md)   
 [Analysis Services 데이터베이스 연결 및 분리](../../analysis-services/multidimensional-models/attach-and-detach-analysis-services-databases.md)   
 [데이터베이스 저장소 위치](../../analysis-services/multidimensional-models/database-storage-location.md)   
 [ReadWriteMode 데이터베이스](../../analysis-services/multidimensional-models/database-readwritemodes.md)   
 [Attach 요소](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/attach-element)   
 [Detach 요소](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/detach-element)   
 [ReadWriteMode 요소](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/readwritemode-element)   
 [DbStorageLocation 요소](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/dbstoragelocation-element)  
  
  
