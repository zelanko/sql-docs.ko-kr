---
title: "Excel 통합 문서에 연결 | Microsoft Docs"
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Excel [Integration Services]"
ms.assetid: d9746318-3669-4ce2-bbb0-4a1bd471c9dd
caps.latest.revision: 22
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 22
---
# Excel 통합 문서에 연결
  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지를 Microsoft Office Excel 통합 문서에 연결하려면 Excel 연결 관리자가 필요합니다.  
  
 이러한 연결 관리자는 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너의 연결 관리자 영역 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가져오기 및 내보내기 마법사에서 만들 수 있습니다.  
  
 **Microsoft Excel 및 Access 파일용 공급자 및 드라이버**  
  
 Microsoft Office 파일용 OLE DB 공급자와 드라이버가 아직 설치되어 있지 않으면 다운로드해야 할 수 있습니다. 최신 버전 공급자는 이전 버전의 Excel에서 만든 파일을 열 수 있습니다.  
  
 컴퓨터에 32비트 버전의 Office가 설치되어 있으면 32비트 버전 드라이버를 설치해야 하며 마법사 또는 마법사에서 생성하는 Integration Services 패키지도 32비트 모드에서 실행해야 합니다.  
  
|Microsoft Office 버전|다운로드|  
|------------------------------|--------------|  
|2007|[2007 Office System 드라이버: 데이터 연결 구성 요소](https://www.microsoft.com/en-us/download/details.aspx?id=23734)|  
|2010|[Microsoft Access 2010 Runtime](https://www.microsoft.com/en-us/download/details.aspx?id=10910)|  
|2013|[Microsoft Access 2013 Runtime](http://www.microsoft.com/en-us/download/details.aspx?id=39358)|  
  
### 연결 관리자 영역에서 Excel 연결 관리자를 만들려면  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 패키지를 엽니다.  
  
2.  **연결 관리자** 영역의 아무 곳이나 마우스 오른쪽 단추로 클릭한 다음 **새 연결**을 선택합니다.  
  
3.  **SSIS 연결 관리자 추가** 대화 상자에서 **Excel**을 선택한 후 연결 관리자를 구성합니다.  
  
     이 연결 관리자에 사용할 수 있는 구성 옵션에 대한 자세한 내용은 [Excel Connection Manager Editor](../../integration-services/connection-manager/excel-connection-manager-editor.md)를 참조하십시오.  
  
### SQL Server 가져오기 및 내보내기 마법사에서 Excel 연결을 만들려면  
  
1.  32비트 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가져오기 및 내보내기 마법사를 시작합니다.  
  
2.  **데이터 원본 선택** 페이지에서 **데이터 원본**에 **Microsoft Excel**을 선택한 다음 Excel 연결을 구성합니다.  
  
     이 연결 형식에 사용할 수 있는 구성 옵션에 대한 자세한 내용은 [Excel Connection Manager Editor](../../integration-services/connection-manager/excel-connection-manager-editor.md)를 참조하십시오.  
  
## 관련 항목:  
 [Access 데이터베이스에 연결](../../integration-services/connection-manager/connect-to-an-access-database.md)  
  
  