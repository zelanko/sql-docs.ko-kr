---
title: "Excel 통합 문서에 연결 | Microsoft Docs"
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: connection-manager
ms.reviewer: 
ms.suite: sql
ms.custom: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Excel [Integration Services]
ms.assetid: d9746318-3669-4ce2-bbb0-4a1bd471c9dd
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 3ece6c4ef032f7b60f82f3f58ee602d0a4ac1196
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/25/2018
---
# <a name="connect-to-an-excel-workbook"></a>Excel 통합 문서에 연결
  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지를 Microsoft Office Excel 통합 문서에 연결하려면 Excel 연결 관리자가 필요합니다.  
  
 이러한 연결 관리자는 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너의 연결 관리자 영역 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가져오기 및 내보내기 마법사에서 만들 수 있습니다.  
 
## <a name="connectivity-components-for-microsoft-excel-and-access-files"></a>Microsoft Excel 및 Access 파일용 연결 구성 요소
  
Microsoft Office 파일용 연결 구성 요소가 아직 설치되지 않은 경우 다운로드해야 할 수 있습니다. [Microsoft Access 데이터베이스 엔진 2016 재배포 가능](https://www.microsoft.com/download/details.aspx?id=54920)에서 최신 버전의 Excel 및 Access 파일용 연결 구성 요소를 다운로드합니다.
  
최신 버전 구성 요소는 이전 버전의 Excel에서 만든 파일을 열 수 있습니다.

컴퓨터에 32비트 버전의 Office가 설치되어 있으면 32비트 버전 구성 요소를 설치해야 하며 패키지도 32비트 모드에서 실행해야 합니다.

Office 365 구독이 있는 경우 Microsoft Access 2016 런타임이 아닌 Access 데이터베이스 엔진 2016 재배포 가능 패키지를 다운로드해야 합니다. 설치 관리자를 실행하는 경우 Office 간편 실행 구성 요소와 함께 다운로드를 설치할 수 없다는 오류 메시지가 표시될 수 있습니다. 이 오류 메시지를 무시하고 구성 요소를 성공적으로 설치하려면 명령 프롬프트 창을 열고 `/quiet` 스위치와 함께 다운로드한 .EXE 파일을 실행하여 자동 모드에서 설치를 실행합니다. 예를 들어 다음과 같이 사용할 수 있습니다.

`C:\Users\<user name>\Downloads\AccessDatabaseEngine.exe /quiet`

## <a name="create-an-excel-connection-manager"></a>Excel 연결 관리자 만들기

### <a name="to-create-an-excel-connection-manager-from-the-connection-managers-area"></a>연결 관리자 영역에서 Excel 연결 관리자를 만들려면  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 패키지를 엽니다.  
  
2.  **연결 관리자** 영역의 아무 곳이나 마우스 오른쪽 단추로 클릭한 다음 **새 연결**을 선택합니다.  
  
3.  **SSIS 연결 관리자 추가** 대화 상자에서 **Excel**을 선택한 후 연결 관리자를 구성합니다.  
  
     이 연결 관리자에 사용할 수 있는 구성 옵션에 대한 자세한 내용은 [Excel Connection Manager Editor](../../integration-services/connection-manager/excel-connection-manager-editor.md)를 참조하십시오.  
  
### <a name="to-create-an-excel-connection-from-the-sql-server-import-and-export-wizard"></a>SQL Server 가져오기 및 내보내기 마법사에서 Excel 연결을 만들려면  
  
1.  32비트 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가져오기 및 내보내기 마법사를 시작합니다.  
  
2.  **데이터 원본 선택** 페이지에서 **데이터 원본**에 **Microsoft Excel**을 선택한 다음 Excel 연결을 구성합니다.  
  
     이 연결 형식에 사용할 수 있는 구성 옵션에 대한 자세한 내용은 [Excel Connection Manager Editor](../../integration-services/connection-manager/excel-connection-manager-editor.md)를 참조하십시오.  
  
## <a name="see-also"></a>참고 항목  
 [Access 데이터베이스에 연결](../../integration-services/connection-manager/connect-to-an-access-database.md)  
  
  
