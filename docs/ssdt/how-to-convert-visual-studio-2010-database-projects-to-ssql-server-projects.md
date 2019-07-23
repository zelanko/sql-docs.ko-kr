---
title: '방법: Visual Studio 2010 데이터베이스 프로젝트를 SQL Server 데이터베이스 프로젝트로 변환 및 다른 플랫폼으로 대상 변경 | Microsoft Docs'
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.topic: conceptual
f1_keywords:
- sql.data.tools.projectconversion.dialog
- sql.data.tools.ImportDAC
ms.assetid: 7e5acf94-5c46-44c7-9ff5-ca7926f5332a
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 84815176ca9b32614e851800a59ea2951010ce4c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67897317"
---
# <a name="how-to-convert-a-visual-studio-2010-database-projects-to-sql-server-database-projects-and-retarget-to-a-different-platform"></a>방법: Visual Studio 2010 데이터베이스 프로젝트를 SQL Server 데이터베이스 프로젝트로 변환 및 다른 플랫폼으로 대상 변경
SSDT(SQL Server Data Tools)에서는 Visual Studio 2010에서 만든 기존의 SQL Server 데이터베이스, CLR 및 데이터 계층 애플리케이션 프로젝트를 새 SQL Server 데이터베이스 프로젝트로 변환할 수 있습니다. 이렇게 하면 SSDT에서 제공하는 업데이트된 Transact\-SQL 편집 환경 등의 새 데이터베이스 개발 환경과 코드 유효성 검사를 통해 프로젝트의 대상을 Microsoft SQL Server 2012 및 SQL Azure로 변경하는 기능을 사용할 수 있습니다. 변환 프로세스에서는 테이블, 뷰, 저장 프로시저, 속성 파일 또는 스크립트 등과 같이 SSDT에 해당하는 형식이 있는 개체를 변환하며 여기에는 해당 권한과 DAC 정책 파일이 포함됩니다. 변환할 수 없는 아티팩트는 변환 로그/보고서에서 강조 표시됩니다.  
  
다음 표에서는 SSDT에서 변환하거나 변환할 수 없는 모든 프로젝트 아티팩트를 보여 줍니다.  
  
|변환할 수 있는 프로젝트 아티팩트|변환할 수 없는 프로젝트 아티팩트|  
|-------------------------------------------|----------------------------------------------|  
|프로젝트 파일<br /><br />.dbproj(Visual Studio 2010 데이터베이스 및 서버 프로젝트, 데이터 계층 응용 프로그램 프로젝트) 프로젝트 파일<br /><br />.csproj 및 .vbproj CLR 프로젝트 파일은 변환할 수는 있지만 데이터가 손실될 수 있습니다.|데이터베이스 단위 테스트 프로젝트<br /><br />부분 프로젝트(예: .files 항목)|  
|속성 파일<br /><br />*.sqldeployment, .sqlsettings 및 .sqlpolicy 파일은 해당하는 프로젝트 속성 페이지로 변환됩니다.<br /><br />.sqlpermissions 파일은 Transact\-SQL 스크립트로 변환됩니다.|프로젝트 속성<br /><br />Server.sqlsettings<br /><br />.sqlcmd 파일에 정의된 SQLCMD 변수|  
|.sql 파일은 기존 폴더 구조를 사용하여 가져오게 됩니다.|확장성 파일|  
|배포 전 및 배포 후 스크립트|프로젝트 변환 후 데이터베이스 참조를 수동으로 다시 설정해야 합니다.|  
|스키마 비교 파일|데이터 생성 파일|  
  
### <a name="to-convert-a-project"></a>프로젝트를 변환하려면  
  
1.  SQL Server 2005 또는 2008 데이터베이스 프로젝트를 엽니다.  
  
2.  **SQL Server 데이터베이스 프로젝트로 변환** 마법사가 자동으로 열립니다. **SQL Server 데이터베이스 프로젝트로 변환**을 선택하고 **확인**을 클릭합니다. 기본 설정을 그대로 사용하여 선택한 기존 파일을 백업합니다.  
  
3.  변환 보고서가 자동으로 생성되고 변환된 모든 파일이 나열됩니다. 변환 프로세스에 대한 추가 정보를 읽으려면 프로젝트 파일 이름 옆의 **+** 기호를 클릭합니다.  
  
4.  **솔루션 탐색기**에서 프로젝트 파일, 속성 파일 및 스키마 개체가 모두 변환되었는지 확인합니다.  
  
### <a name="to-change-a-projects-target-platform"></a>프로젝트의 대상 플랫폼을 변경하려면  
  
1.  **솔루션 탐색기**에서 새로 변환된 프로젝트를 마우스 오른쪽 단추로 클릭하고 **속성**을 선택하여 **프로젝트 설정** 대화 상자에 액세스합니다.  
  
2.  **대상 플랫폼** 드롭다운 목록에서 SSDT 지원 플랫폼 중 하나를 선택합니다.  
  
## <a name="see-also"></a>참고 항목  
[방법: 대상 플랫폼 변경 및 데이터베이스 프로젝트 게시](../ssdt/how-to-change-target-platform-and-publish-a-database-project.md)  
  
