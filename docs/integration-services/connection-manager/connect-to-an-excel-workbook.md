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
caps.latest.revision: 22
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 2800075091835b2d6f2b07ee34e9b897fe86634e
ms.openlocfilehash: f8fb1db80ac1b750950a3401516b54af5ee29686
ms.contentlocale: ko-kr
ms.lasthandoff: 08/17/2017

---
# <a name="connect-to-an-excel-workbook"></a>Excel 통합 문서에 연결
  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지를 Microsoft Office Excel 통합 문서에 연결하려면 Excel 연결 관리자가 필요합니다.  
  
 이러한 연결 관리자는 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너의 연결 관리자 영역 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가져오기 및 내보내기 마법사에서 만들 수 있습니다.  
 
## <a name="connectivity-components-for-microsoft-excel-and-access-files"></a>Microsoft Excel 및 Access 파일에 대 한 연결 구성 요소
  
설치 되어 있지 않으면 Microsoft Office 파일에 대 한 연결 구성 요소를 다운로드 해야 할 수 있습니다. 최신 버전의 Excel 및 Access 모두 파일에 여기에 대 한 연결 구성 요소 다운로드: [Microsoft Access 데이터베이스 엔진 2016 재배포 가능 패키지](https://www.microsoft.com/download/details.aspx?id=54920)합니다.
  
최신 버전의 구성 요소는 이전 버전의 Excel에서 만든 파일을 열 수 있습니다.

컴퓨터에 32 비트 버전의 Office가 32 비트 버전의 구성 요소를 설치 해야 합니다 및 32 비트 모드로 패키지를 실행 해야 합니다.

Office 365 구독을 보유 하는 경우 Access 데이터베이스 엔진 2016 재배포 가능 패키지 및 Microsoft Access 2016 런타임이 아닌를 다운로드 해야 합니다. 설치 관리자를 실행 하는 경우 Office 간편 실행 구성 요소와는 다운로드-함께 설치할 수 없습니다 오류 메시지가 표시 될 수 있습니다. 이 오류 메시지를 무시 하 고 구성 요소를 성공적으로 설치 하려면 설치 자동 모드로 명령 프롬프트 창을 열고 실행 하 여 실행 된 합니다. 와 함께 다운로드 한 EXE 파일의 `/quiet` 전환 합니다. 예를 들어

`C:\Users\<user name>\Downloads\AccessDatabaseEngine.exe /quiet`

## <a name="create-an-excel-connection-manager"></a>Excel 연결 관리자를 만듭니다.

### <a name="to-create-an-excel-connection-manager-from-the-connection-managers-area"></a>연결 관리자 영역에서 Excel 연결 관리자를 만들려면  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 패키지를 엽니다.  
  
2.  **연결 관리자** 영역의 아무 곳이나 마우스 오른쪽 단추로 클릭한 다음 **새 연결**을 선택합니다.  
  
3.  **SSIS 연결 관리자 추가** 대화 상자에서 **Excel**을 선택한 후 연결 관리자를 구성합니다.  
  
     이 연결 관리자에 사용할 수 있는 구성 옵션에 대한 자세한 내용은 [Excel Connection Manager Editor](../../integration-services/connection-manager/excel-connection-manager-editor.md)를 참조하십시오.  
  
### <a name="to-create-an-excel-connection-from-the-sql-server-import-and-export-wizard"></a>SQL Server 가져오기 및 내보내기 마법사에서 Excel 연결을 만들려면  
  
1.  32비트 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가져오기 및 내보내기 마법사를 시작합니다.  
  
2.  **데이터 원본 선택** 페이지에서 **데이터 원본**에 **Microsoft Excel**을 선택한 다음 Excel 연결을 구성합니다.  
  
     이 연결 형식에 사용할 수 있는 구성 옵션에 대한 자세한 내용은 [Excel Connection Manager Editor](../../integration-services/connection-manager/excel-connection-manager-editor.md)를 참조하십시오.  
  
## <a name="see-also"></a>관련 항목:  
 [Access 데이터베이스에 연결](../../integration-services/connection-manager/connect-to-an-access-database.md)  
  
  

