---
title: "Excel 연결 관리자 | Microsoft Docs"
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: connection-manager
ms.reviewer: 
ms.suite: sql
ms.custom: 
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.dts.designer.excelconnection.f1
helpviewer_keywords:
- files [Integration Services], connections
- connections [Integration Services], Excel
- Excel [Integration Services]
- connection managers [Integration Services], Excel
ms.assetid: 667419f2-74fb-4b50-b963-9197d1368cda
caps.latest.revision: "41"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 5785a2753b61cde59a5ed157d697b05a93796fc7
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/20/2017
---
# <a name="excel-connection-manager"></a>Excel 연결 관리자
  Excel 연결 관리자를 사용하면 패키지에서 기존 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Excel 통합 문서 파일에 연결할 수 있습니다. [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 에 포함되는 Excel 원본과 Excel 대상에서 Excel 연결 관리자가 사용됩니다.  
  
 패키지에 Excel 연결 관리자를 추가하면 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 에서 런타임에 Excel 연결로 확인되는 연결 관리자를 만들고, 연결 관리자 속성을 설정하고, 연결 관리자를 패키지의 **Connections** 컬렉션에 추가합니다.  
  
 연결 관리자의 **ConnectionManagerType** 속성이 **EXCEL**로 설정됩니다.  
  
## <a name="configuration-of-the-excel-connection-manager"></a>Excel 연결 관리자 구성  
 다음과 같은 방법으로 Excel 연결 관리자를 구성할 수 있습니다.  
  
-   Excel 통합 문서 파일의 경로를 지정합니다.  
  
    > [!NOTE]  
    >  암호로 보호된 Excel 파일에는 연결할 수 없습니다.  
  
-   파일을 만드는 데 사용된 Excel 버전을 지정합니다.  
  
-   선택한 워크시트 또는 범위에서 액세스한 첫 데이터 행에 열 이름이 포함되는지 여부를 나타냅니다.  
  
 Excel 연결 관리자가 Excel 원본에 사용될 경우 열 이름이 추출한 데이터에 포함됩니다. Excel 대상에 사용될 경우에는 열 이름이 기록된 데이터에 포함됩니다.  
  
 Excel 원본 및 Excel 대상의 동작에 대한 자세한 내용은 [Excel Source](../../integration-services/data-flow/excel-source.md) 및 [Excel Destination](../../integration-services/data-flow/excel-destination.md)을(를) 참조하십시오.  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너를 사용하거나 프로그래밍 방식으로 속성을 설정할 수 있습니다.  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너에서 설정할 수 있는 속성에 대한 자세한 내용은 [Excel 연결 관리자 편집기](../../integration-services/connection-manager/excel-connection-manager-editor.md)를 참조하세요.  
  
 연결 관리자를 프로그래밍 방식으로 구성하는 방법에 대한 자세한 내용은 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> 및 [프로그래밍 방식으로 연결 추가](../../integration-services/building-packages-programmatically/adding-connections-programmatically.md)로 설정됩니다.  
  
 Excel 파일 그룹을 통한 루핑 방법에 대한 자세한 내용은 [Foreach 루프 컨테이너를 사용하여 Excel 파일 및 테이블 루핑](../../integration-services/control-flow/loop-through-excel-files-and-tables-by-using-a-foreach-loop-container.md)을 참조하세요.  
  
## <a name="excel-connection-manager-editor"></a>Excel 연결 관리자 편집기
  **Excel 연결 관리자 편집기** 대화 상자를 사용하여 기존 또는 새 [!INCLUDE[ofprexcel](../../includes/ofprexcel-md.md)] 통합 문서 파일에 대한 연결을 추가할 수 있습니다.  
  
 Excel 연결 관리자에 대한 자세한 내용은 [Excel Connection Manager](../../integration-services/connection-manager/excel-connection-manager.md)를 참조하십시오.  
  
### <a name="options"></a>옵션  
 **Excel 파일 경로**  
 기존 또는 새 Excel 통합 문서 파일(.xls)의 경로와 파일 이름을 입력합니다.  
  
> [!NOTE]  
>  암호로 보호된 Excel 파일에는 연결할 수 없습니다.  
  
> [!WARNING]  
>  새로 만들거나 존재하지 않는 파일을 가리키는 **Excel 연결** 을 선택한 다음 **Excel 시트의 이름** 에서 **새로 만들기** 를 클릭하면 **Excel 대상 편집기**에서 Excel 파일을 자동으로 만듭니다.  
  
 **찾아보기**  
 **열기** 대화 상자를 사용하여 Excel 파일이 있는 폴더 또는 새 파일을 만들려는 폴더로 이동합니다.  
  
 **Excel 버전**  
 파일을 만드는 데 사용된 Microsoft Excel 버전을 지정합니다.  
  
 **첫 행은 열 이름으로**  
 선택한 워크시트의 첫 데이터 행에 열 이름이 포함되는지 여부를 지정합니다. 이 옵션의 기본값은 **True**입니다.  
  
## <a name="connectivity-components-for-microsoft-excel-and-access-files"></a>Microsoft Excel 및 Access 파일용 연결 구성 요소
  
Microsoft Office 파일용 연결 구성 요소가 아직 설치되지 않은 경우 다운로드해야 할 수 있습니다. [Microsoft Access 데이터베이스 엔진 2016 재배포 가능](https://www.microsoft.com/download/details.aspx?id=54920)에서 최신 버전의 Excel 및 Access 파일용 연결 구성 요소를 다운로드합니다.
  
최신 버전 구성 요소는 이전 버전의 Excel에서 만든 파일을 열 수 있습니다.

컴퓨터에 32비트 버전의 Office가 설치되어 있으면 32비트 버전 구성 요소를 설치해야 하며 패키지도 32비트 모드에서 실행해야 합니다.

Office 365 구독을 보유하는 경우 Microsoft Access 2016 런타임이 아닌 Access 데이터베이스 엔진 2016 재배포 가능을 다운로드해야 합니다. 설치 관리자를 실행하는 경우 Office 간편 실행 구성 요소와 함께 다운로드를 설치할 수 없다는 오류 메시지가 표시될 수 있습니다. 이 오류 메시지를 무시하려면 명령 프롬프트 창을 열고 `/quiet` 스위치와 함께 다운로드한 .EXE 파일을 실행하여 자동 모드에서 설치를 실행합니다. 예를 들어

`C:\Users\<user name>\Downloads\AccessDatabaseEngine.exe /quiet`
  
## <a name="related-tasks"></a>관련 태스크  
  
-   [Foreach 루프 컨테이너를 사용하여 Excel 파일 및 테이블 루핑](../../integration-services/control-flow/loop-through-excel-files-and-tables-by-using-a-foreach-loop-container.md)  
  
-   [Excel 통합 문서에 연결](../../integration-services/connection-manager/connect-to-an-excel-workbook.md)  
  
  
