---
title: '방법: 배포 전 또는 배포 후 스크립트 지정 | Microsoft Docs'
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 7f78f517-f13d-4f4b-84b9-e804cb490b2c
author: markingmyname
ms.author: maghan
ms.openlocfilehash: a1531bffd50bb14838e74b5315c30a870563f86f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68035013"
---
# <a name="how-to-specify-predeployment-or-postdeployment-scripts"></a>방법: 배포 전 또는 배포 후 스크립트 지정
배포 전 및 배포 후 스크립트는 데이터베이스 프로젝트에서 생성되는 주 배포 스크립트 이전과 이후에 Transact\-SQL 문을 실행합니다. 프로젝트에는 배포 전 스크립트와 배포 후 스크립트가 각각 하나씩만 포함될 수 있습니다. 이러한 스크립트는 다양한 용도로 사용할 수 있습니다. 예를 들어  
  
-   배포 전 스크립트는 변경할 테이블에 있는 데이터의 서식을 다시 지정하고 해당 데이터를 배포 후 스크립트의 변경된 테이블에 적용하기 전에 임시 테이블로 복사할 수 있습니다.  
  
-   배포 후 스크립트의 테이블에 있어야 하는 참조 데이터를 삽입할 수 있습니다. 데이터를 삽입하기 전에 해당 테이블에 이미 데이터가 포함되어 있는지 테스트할 수 있습니다. 테이블이 비어 있지 않으면 기존 데이터를 지우거나 배포 전에 데이터베이스를 항상 다시 만들도록 지정해야 합니다. 다음과 같은 문을 배포 후 스크립트에 추가할 수 있습니다.  
  
```  
IF (EXISTS(SELECT * FROM [dbo].[MyReferenceTable]))  
BEGIN  
    DELETE FROM [dbo].[MyReferenceTable]  
END  
```  
  
## <a name="to-add-and-modify-a-pre--or-post-deployment-script"></a>배포 전 스크립트 또는 배포 후 스크립트를 추가하거나 수정하려면  
  
1.  **솔루션 탐색기**에서 데이터베이스 프로젝트를 확장하여 스크립트 폴더를 표시합니다.  
  
2.  스크립트 폴더를 마우스 오른쪽 단추로 클릭하고 추가를 선택합니다.  
  
3.  상황에 맞는 메뉴에서 스크립트를 선택합니다.  
  
4.  배포 전 스크립트 또는 배포 후 스크립트를 선택합니다. 필요에 따라 기본값이 아닌 이름을 지정합니다. 추가를 클릭하여 작업을 마칩니다.  
  
5.  스크립트 폴더에서 파일을 두 번 클릭합니다.  
  
    Transact\-SQL 편집기가 열리고 파일 내용이 표시됩니다.  
  
스크립트에 SQLCMD 구문 및 변수를 사용하고 이러한 구문과 변수를 데이터베이스 프로젝트 속성에 설정할 수 있습니다. 예를 들어  
  
-   SQLCMD 구문을 사용하여 파일 내용을 배포 전 스크립트 또는 배포 후 스크립트에 포함할 수 있습니다. 파일은 정의하는 순서대로 포함되고 실행됩니다(`:r .\myfile.sql`).  
  
-   SQLCMD 구문을 사용하여 배포 후 스크립트의 변수를 참조할 수 있습니다. SQLCMD 변수를 프로젝트 속성 또는 게시 프로필에 설정할 수 있습니다.  
  
    ```  
    :setvar TableName MyTable  
    SELECT * FROM [$(TableName)]  
    ```  
  
스크립트에서 SQLCMD를 사용하는 방법에 대한 자세한 내용은 [데이터베이스 프로젝트 설정](../ssdt/database-project-settings.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
[프로젝트 기반 오프라인 데이터베이스 개발](../ssdt/project-oriented-offline-database-development.md)  
  
