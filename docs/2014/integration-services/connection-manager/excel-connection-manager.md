---
title: Excel 연결 관리자 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
helpviewer_keywords:
- files [Integration Services], connections
- connections [Integration Services], Excel
- Excel [Integration Services]
- connection managers [Integration Services], Excel
ms.assetid: 667419f2-74fb-4b50-b963-9197d1368cda
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: aa7bc6280afeb9bce7525afc3eb5eb19c73e4c01
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48183913"
---
# <a name="excel-connection-manager"></a>Excel 연결 관리자
  Excel 연결 관리자를 사용하면 패키지에서 기존 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Excel 통합 문서 파일에 연결할 수 있습니다. Excel 원본과 Excel 대상입니다 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 포함 Excel 연결 관리자를 사용 합니다.  
  
 패키지에 Excel 연결 관리자를 추가하면 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]에서 런타임에 Excel 연결로 확인되는 연결 관리자를 만들고, 연결 관리자 속성을 설정하고, 연결 관리자를 패키지의 `Connections` 컬렉션에 추가합니다.  
  
 합니다 `ConnectionManagerType` 연결 관리자의 속성이 `EXCEL`합니다.  
  
> [!NOTE]  
>  암호로 보호된 Excel 파일에는 연결할 수 없습니다.  
  
## <a name="configuration-of-the-excel-connection-manager"></a>Excel 연결 관리자 구성  
 다음과 같은 방법으로 Excel 연결 관리자를 구성할 수 있습니다.  
  
-   Excel 통합 문서 파일의 경로를 지정합니다.  
  
-   파일을 만드는 데 사용된 Excel 버전을 지정합니다.  
  
-   선택한 워크시트 또는 범위에서 액세스한 첫 데이터 행에 열 이름이 포함되는지 여부를 나타냅니다.  
  
 Excel 연결 관리자가 Excel 원본에 사용될 경우 열 이름이 추출한 데이터에 포함됩니다. Excel 대상에 사용될 경우에는 열 이름이 기록된 데이터에 포함됩니다.  
  
 Excel 연결 관리자는 Jet 4.0용 [!INCLUDE[msCoName](../../includes/msconame-md.md)] OLE DB 공급자와 공급자에서 지원하는 Excel ISAM(Indexed Sequential Access Method) 드라이버를 사용하여 Excel 데이터 원본에 연결하고 데이터를 읽고 씁니다. 이 공급자와 드라이버 Excel 원본과 Excel 대상을 사용 하는 경우의 동작에 대 한 자세한 내용은 참조 [Excel 원본](../data-flow/excel-source.md) 하 고 [Excel 대상](../data-flow/excel-destination.md)합니다.  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너를 사용하거나 프로그래밍 방식으로 속성을 설정할 수 있습니다.  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너에서 설정할 수 있는 속성에 대한 자세한 내용은 [Excel 연결 관리자 편집기](../excel-connection-manager-editor.md)를 참조하세요.  
  
 연결 관리자를 프로그래밍 방식으로 구성 하는 방법에 대 한 내용은 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> 하 고 [프로그래밍 방식으로 연결 추가](../building-packages-programmatically/adding-connections-programmatically.md)합니다.  
  
 Excel 파일 그룹을 통한 루핑 방법에 대한 자세한 내용은 [Foreach 루프 컨테이너를 사용하여 Excel 파일 및 테이블 루핑](../control-flow/foreach-loop-container.md)을 참조하세요.  
  
## <a name="related-tasks"></a>관련 작업  
  
-   [Foreach 루프 컨테이너를 사용하여 Excel 파일 및 테이블 루핑](../control-flow/foreach-loop-container.md)  
  
-   [SSIS(SQL Server Integration Services)를 사용하여 Excel에서 데이터 가져오기 또는 Excel로 데이터 내보내기](../load-data-to-from-excel-with-ssis.md)
  
  
