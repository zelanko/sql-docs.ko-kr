---
title: "Excel 연결 관리자 편집기 | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/02/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.excelconnection.f1"
helpviewer_keywords: 
  - "Excel 연결 관리자 편집기"
ms.assetid: 7ff097e4-cafb-4885-a898-05b2a46628c1
caps.latest.revision: 32
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 32
---
# Excel 연결 관리자 편집기
  **Excel 연결 관리자 편집기** 대화 상자를 사용하여 기존 또는 새 [!INCLUDE[ofprexcel](../../includes/ofprexcel-md.md)] 통합 문서 파일에 대한 연결을 추가할 수 있습니다.  
  
 Excel 연결 관리자에 대한 자세한 내용은 [Excel Connection Manager](../../integration-services/connection-manager/excel-connection-manager.md)를 참조하십시오.  
  
## 옵션  
 **Excel 파일 경로**  
 기존 또는 새 Excel 통합 문서 파일(.xls)의 경로와 파일 이름을 입력합니다.  
  
> [!NOTE]  
>  암호로 보호된 Excel 파일에는 연결할 수 없습니다.  
  
> [!WARNING]  
>  새로 만들거나 존재하지 않는 파일을 가리키는 **Excel 연결**을 선택한 다음 **Excel 시트의 이름**에서 **새로 만들기**를 클릭하면 **Excel 대상 편집기**에서 Excel 파일을 자동으로 만듭니다.  
  
 **찾아보기**  
 **열기** 대화 상자를 사용하여 Excel 파일이 있는 폴더 또는 새 파일을 만들려는 폴더로 이동합니다.  
  
 **Excel 버전**  
 파일을 만드는 데 사용된 Microsoft Excel 버전을 지정합니다.  
  
 **첫 행은 열 이름으로**  
 선택한 워크시트의 첫 데이터 행에 열 이름이 포함되는지 여부를 지정합니다. 이 옵션의 기본값은 **True**입니다.  
  
## Microsoft Excel 및 Access 파일용 공급자 및 드라이버  
 Microsoft Office 파일용 OLE DB 공급자와 드라이버가 아직 설치되어 있지 않으면 다운로드해야 할 수 있습니다. 최신 버전 공급자는 이전 버전의 Excel에서 만든 파일을 열 수 있습니다.  
  
 컴퓨터에 32비트 버전의 Office가 설치되어 있으면 32비트 버전 드라이버를 설치해야 하며 마법사 또는 마법사에서 생성하는 Integration Services 패키지도 32비트 모드에서 실행해야 합니다.  
  
|Microsoft Office 버전|다운로드|  
|------------------------------|--------------|  
|2007|[2007 Office System 드라이버: 데이터 연결 구성 요소](https://www.microsoft.com/download/details.aspx?id=23734)|  
|2010|[Microsoft Access 2010 Runtime](https://www.microsoft.com/download/details.aspx?id=10910)|  
|2013|[Microsoft Access 2013 Runtime](http://www.microsoft.com/download/details.aspx?id=39358)|  
|2016|[Microsoft Access 2016 Runtime](https://www.microsoft.com/download/details.aspx?id=50040)|
  
## 관련 항목:  
 [Integration Services 오류 및 메시지 참조](../../integration-services/integration-services-error-and-message-reference.md)   
 [Foreach 루프 컨테이너를 사용하여 Excel 파일 및 테이블 루핑](../../integration-services/control-flow/loop-through-excel-files-and-tables-by-using-a-foreach-loop-container.md)  
  
  