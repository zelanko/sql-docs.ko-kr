---
title: "Access 데이터베이스에 연결 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Access [Integration Services]
- Access databases [Integration Services]
ms.assetid: 229fbd46-ef6a-4609-a4cc-d80d52c33cf1
caps.latest.revision: 18
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: e6fe201622d38c10967c9c076da0d99d215ea33f
ms.contentlocale: ko-kr
ms.lasthandoff: 08/03/2017

---
# <a name="connect-to-an-access-database"></a>Access 데이터베이스에 연결
  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지를 Microsoft Office Access 데이터 원본에 연결하려면 OLE DB 연결 관리자와 데이터 공급자가 필요합니다. 사용되는 데이터 공급자는 다음과 같이 데이터 원본을 만든 Access의 버전에 따라 달라집니다.  
  
-   Access 2003 및 그 이전 버전의 경우 패키지에는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Jet OLE DB 공급자가 필요합니다.  
  
-   Access 2007의 경우 패키지에는 Microsoft Office 12.0 Access Database Engine OLE DB Provider가 필요합니다.  
  
 OLE DB 연결 관리자를 만들고 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너의 연결 관리자 영역 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가져오기 및 내보내기 마법사에서 해당 데이터 공급자를 선택할 수 있습니다.  
  
> [!NOTE]  
>  64비트 컴퓨터에서는 32비트 모드로 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Access 데이터 원본에 연결되는 패키지를 실행해야 합니다. [!INCLUDE[msCoName](../../includes/msconame-md.md)] Jet OLE DB 공급자와 Microsoft Office 12.0 Access Database Engine OLE DB Provider는 모두 32비트 버전만 사용할 수 있습니다.  
  
## <a name="connecting-to-a-data-source-in-access-2003-or-earlier-format"></a>Access 2003 또는 그 이전 형식의 데이터 원본에 연결  
  
#### <a name="to-create-an-access-connection-manager-from-the-connection-managers-area"></a>연결 관리자 영역에서 Access 연결 관리자를 만들려면  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 패키지를 엽니다.  
  
2.  **연결 관리자** 영역의 아무 곳이나 마우스 오른쪽 단추로 클릭한 다음 **새 OLE DB 연결**을 선택합니다.  
  
3.  **OLE DB 연결 관리자 구성** 대화 상자에서 **새로 만들기**를 클릭합니다.  
  
     자세한 내용은 [OLE DB Connection Manager](../../integration-services/connection-manager/ole-db-connection-manager.md)를 참조하세요.  
  
4.  **연결 관리자** 대화 상자에서 **공급자**에 **Microsoft Jet 4.0 OLE DB Provider**를 선택한 다음 연결 관리자를 적절히 구성합니다.  
  
#### <a name="to-create-an-access-connection-from-the-sql-server-import-and-export-wizard"></a>SQL Server 가져오기 및 내보내기 마법사에서 Access 연결을 만들려면  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가져오기 및 내보내기 마법사를 시작합니다.  
  
2.  **데이터 원본 선택** 페이지에서 **데이터 원본**에 **Microsoft Access**를 선택한 다음 Access 연결을 구성합니다.  
  
     **데이터 원본** 으로 **Microsoft Access**를 선택하면 마법사는 올바른 데이터 공급자를 사용하여 필요한 OLE DB 연결 관리자를 자동으로 만듭니다. 자세한 내용은 [OLE DB Connection Manager](../../integration-services/connection-manager/ole-db-connection-manager.md)를 참조하세요.  
  
## <a name="connecting-to-a-data-source-in-access-2007-format"></a>Access 2007 형식의 데이터 원본에 연결  
 Access 2007 데이터 원본에 액세스하려면 OLE DB 연결 관리자에서 Microsoft Office 12.0 Access Database Engine OLE DB Provider가 필요합니다. 이 공급자는 2007 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office system과 함께 자동으로 설치됩니다. [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 가 실행 중인 컴퓨터에 2007 Office system이 설치되어 있지 않은 경우 공급자를 별도로 설치해야 합니다. Microsoft Office 12.0 Access Database Engine OLE DB Provider를 설치하려면 웹 페이지 [2007 Office System 드라이버: 데이터 연결 구성 요소](http://go.microsoft.com/fwlink/?LinkId=98155)에서 구성 요소를 다운로드하여 설치합니다.  
  
#### <a name="to-create-an-ole-db-connection-manager-from-the-connection-managers-area"></a>연결 관리자 영역에서 OLE DB 연결 관리자를 만들려면  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 패키지를 엽니다.  
  
2.  **연결 관리자** 영역의 아무 곳이나 마우스 오른쪽 단추로 클릭한 다음 **새 OLE DB 연결**을 선택합니다.  
  
3.  **OLE DB 연결 관리자 구성** 대화 상자에서 **새로 만들기**를 클릭합니다.  
  
     자세한 내용은 [OLE DB Connection Manager](../../integration-services/connection-manager/ole-db-connection-manager.md)를 참조하세요.  
  
4.  **연결 관리자** 대화 상자에서 **공급자**에 **Microsoft Office 12.0 Access 데이터베이스 엔진 OLE DB**를 선택한 다음 연결 관리자를 적절히 구성합니다.  
  
    > [!NOTE]  
    >  Access 2007을 사용하는 데이터 원본에 연결하려는 경우 **데이터 원본** 으로 **Microsoft Jet 4.0 OLE DB Provider**는 선택할 수 없습니다.  
  
#### <a name="to-create-an-ole-db-connection-from-the-sql-server-import-and-export-wizard"></a>SQL Server 가져오기 및 내보내기 마법사에서 OLE DB 연결을 만들려면  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가져오기 및 내보내기 마법사를 시작합니다.  
  
2.  **데이터 원본 선택** 페이지에서 **데이터 원본**에 **Microsoft Office 12.0 Access Database Engine OLE DB Provider**를 선택한 다음 연결을 적절히 구성합니다.  
  
    > [!NOTE]  
    >  Access 2007을 사용하는 데이터 원본에 연결하려는 경우 **데이터 원본** 으로 **Microsoft Jet 4.0 OLE DB Provider**는 선택할 수 없습니다.  
  
     **데이터 원본** 으로 **Microsoft Office 12.0 Access Database Engine OLE DB Provider**를 선택하면 마법사는 올바른 데이터 공급자를 사용하여 필요한 OLE DB 연결 관리자를 자동으로 만듭니다. 자세한 내용은 [OLE DB Connection Manager](../../integration-services/connection-manager/ole-db-connection-manager.md)를 참조하세요.  
  
## <a name="see-also"></a>관련 항목:  
 [Excel 통합 문서에 연결](../../integration-services/connection-manager/connect-to-an-excel-workbook.md)  
  
  
