---
title: 테이블 복사 또는 쿼리 지정(SQL Server 가져오기 및 내보내기 마법사) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.impexpwizard.specifytablecopyorquery.f1
ms.assetid: 08aa7158-40e6-4ef3-84d3-1265a8ba194c
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 53d97adb5252594bb38f85989e87742a557331ec
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52750405"
---
# <a name="specify-table-copy-or-query-sql-server-import-and-export-wizard"></a>테이블 복사 또는 쿼리 지정(SQL Server 가져오기 및 내보내기 마법사)
  사용 된 **테이블 복사 또는 쿼리 지정** 페이지 데이터를 복사 하는 방법을 지정 합니다. 그래픽 인터페이스를 사용하여 복사할 기존 데이터베이스 개체를 선택하거나 Transact-SQL을 사용하여 복잡한 쿼리를 만들 수 있습니다.  
  
 이 마법사에 대 한 자세한 내용은 참조 하세요 [SQL Server 가져오기 및 내보내기 마법사](import-and-export-data-with-the-sql-server-import-and-export-wizard.md)합니다. 마법사를 성공적으로 실행 하는 데 필요한 사용 권한 뿐만 아니라 마법사 시작 옵션을 알아보려면 [SQL Server 가져오기 및 내보내기 마법사를 실행](start-the-sql-server-import-and-export-wizard.md)합니다.  
  
 SQL Server 가져오기 및 내보내기 마법사의 목적은 원본에서 대상으로 데이터를 복사하는 것입니다. 이 마법사는 대상 데이터베이스 및 대상 테이블도 만들 수 있습니다. 그러나 여러 개의 데이터베이스 또는 테이블을 복사하거나 다른 종류의 데이터베이스 개체를 복사할 경우 대신 데이터베이스 복사 마법사를 사용해야 합니다. 자세한 내용은 [Use the Copy Database Wizard](../../relational-databases/databases/use-the-copy-database-wizard.md)을 참조하세요.  
  
## <a name="options"></a>변수  
 **하나 이상의 테이블 또는 뷰에서 데이터 복사**  
 필드를 사용 하 여 지정 된 대상 또는 대상에 선택한 원본 테이블 및 뷰를 복사 합니다 **원본 테이블 및 뷰 선택** 대화 상자. 레코드를 필터링하거나 순서를 지정하지 않고 원본의 모든 데이터를 복사하려면 이 옵션을 사용합니다.  
  
 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 데이터 공급자를 사용하여 데이터 원본에 연결하면 **하나 이상의 테이블 또는 뷰에서 데이터 복사** 옵션을 사용하지 못할 수 있습니다. 이 옵션은 ProviderDescriptors.xml 파일에 ProviderDescription 섹션이 있는 공급자에 대해서만 사용할 수 있습니다. 각 ProviderDescription 섹션에는 해당 공급자에서 메타데이터를 검색하는 데 필요한 정보가 포함되어 있습니다. 기본적으로 다음 공급자에 대해서만 ProviderDescriptors.xml 파일에 ProviderDescription 섹션이 포함됩니다.  
  
-   System.Data.SqlClient  
  
-   System.Data.OracleClient  
  
-   System.Data.OleDb  
  
-   System.Data.Odbc  
  
 있도록를 **하나 이상의 테이블 또는 뷰에서 데이터 복사** 추가 공급자에 대 한 사용 가능한 옵션에서 타사 ProviderDescriptors.xml 파일에 자체 ProviderDescriptor 섹션을 추가할 수 있습니다. 기본적으로이 파일은 \< *드라이브*>: \Program Files\Microsoft SQL server\100\dts\providerdescriptors에 있습니다. ProviderDescriptor 섹션에 대한 요구 사항을 검토하려면 기본적으로 ProviderDescriptors.xml 파일과 같은 폴더에 있는 ProviderDescriptors.xsd 스키마 파일을 참조하십시오.  
  
 **전송 데이터를 지정할 쿼리 작성**  
 사용 하 여 행을 검색할 SQL 문을 작성 합니다 **원본 쿼리 제공** 대화 상자. 복사 작업 중에 원본 데이터를 수정하거나 제한하려면 이 옵션을 사용합니다. 선택 조건에 일치하는 행만 복사할 수 있습니다.  
  
  
