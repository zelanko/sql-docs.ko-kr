---
title: "dBASE 또는 다른 DBF 파일에 연결 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: connection-manager
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- connecting to DBF files
- dBase files
- DBF files
ms.assetid: b0e8c831-9f96-475c-82a4-4f5b02692752
caps.latest.revision: "16"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 60fc92f8283ec9b4952152aca6b1e0a5d31a1e6d
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/20/2017
---
# <a name="connect-to-a-dbase-or-other-dbf-file"></a>dBASE 또는 다른 DBF 파일에 연결
  OLE DB 연결 관리자를 사용하고 Microsoft OLE DB Provider for Jet 4.0을 선택하여 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지의 dBASE 또는 다른 .DBF 데이터베이스에 연결할 수 있습니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 SQL Server 가져오기 및 내보내기 마법사에서는 dBASE 또는 다른 DBF 파일에서 데이터를 가져오거나 해당 파일로 데이터를 내보낼 수 없습니다. Microsoft Access 또는 Microsoft Excel을 사용하여 DBF 파일의 데이터를 Access 데이터베이스나 Excel 스프레드시트로 가져온 다음 SQL Server 가져오기 및 내보내기 마법사를 사용할 수 있습니다.  
  
### <a name="to-configure-a-connection-manager-to-connect-to-a-dbase-or-other-dbf-file"></a>dBASE 또는 다른 DBF 파일에 연결하도록 연결 관리자를 구성하려면  
  
1.  패키지에 새 OLE DB 연결 관리자를 추가합니다. 자세한 내용은 [Add, Delete, or Share a Connection Manager in a Package](http://msdn.microsoft.com/library/6f2ba4ea-10be-4c40-9e80-7efcf6ee9655)을 참조하세요.  
  
2.  **연결 관리자** 대화 상자의 **연결** 페이지에서 **공급자**로 네이티브 OLE DB\Microsoft Jet 4.0 OLE DB 공급자를 선택합니다.  
  
3.  DBF 파일을 사용하는 경우 폴더는 데이터베이스를 나타내고 개별 DBF 파일은 테이블을 나타냅니다. 따라서 **데이터베이스 파일 이름** 입력란에는 DBF 파일이 있는 폴더의 경로가 포함되고 파일 이름은 포함되지 않아야 합니다. 폴더 경로를 입력하거나 붙여넣을 수도 있고, **찾아보기** 단추를 사용하여 DBF 파일을 선택한 다음 폴더 경로의 끝에서 파일 이름을 제거할 수도 있습니다.  
  
4.  **연결 관리자** 대화 상자의 **모두** 페이지에서 확장 속성 값으로 **dBASE III**, **dBASE IV**또는 **dBASE 5.0**를 적절하게 입력합니다.  
  
5.  **연결 테스트** 를 클릭하여 입력한 값의 유효성을 검사합니다. "연결 테스트에 성공했습니다."라는 메시지가 표시되면 **확인** 을 클릭하여 메시지 상자를 닫습니다.  
  
6.  **확인** 을 클릭하여 연결 관리자의 구성을 저장합니다.  
  
7.  패키지의 데이터 흐름에서 연결 관리자를 사용하려면 OLE DB 원본이나 대상을 선택하고 이전 단계를 사용하여 만든 연결 관리자를 사용하도록 구성합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [OLE DB 연결 관리자](../../integration-services/connection-manager/ole-db-connection-manager.md)  
  
  
