---
title: 대량 로드 보안 고려 사항 (SQLXML)
description: SQLXML 4.0에서 XML 대량 로드를 사용 하기 위한 보안 지침에 대해 알아봅니다.
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- SQLXML, XML Bulk Load
- bulk load [SQLXML], security
- security [SQLXML], XML Bulk Load
- XML Bulk Load [SQLXML], security
ms.assetid: 192fc6d4-ecbc-4a4d-a5cb-55e1f64af318
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: ec361c23bfd946aaf47e817030237f80cdc4a3ef
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97482944"
---
# <a name="bulk-load-security-considerations-sqlxml-40"></a>대량 로드 보안 고려 사항(SQLXML 4.0)
[!INCLUDE [SQL Server Azure SQL Database](../../../includes/applies-to-version/sql-asdb.md)]
  다음은 XML 대량 로드를 사용하기 위한 보안 지침입니다.  
  
-   대량 로드 작업을 트랜잭션으로 수행 하도록 지정 하는 경우 **Tempfilepath** 속성을 사용 하 여 임시 파일을 만들 폴더를 지정 합니다.  
  
     대량 로드 프로세스에서는 이러한 임시 파일을 다음과 같은 사용 권한으로 만듭니다.  
  
    -   읽기/쓰기/삭제 액세스 권한이 대량 로드 프로세스에 부여됩니다.  
  
    -   Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]가 이러한 파일에 액세스하는 데 사용할 계정을 알 수 없으므로 모든 사용자에게 읽기 권한이 부여됩니다. 이러한 임시 파일이 포함된 폴더에 대해 적절한 사용 권한을 설정하여 이 파일에 대한 액세스를 제한할 수 있습니다.  
  
-   XML 대량 로드 자체에는 사용 권한 설정이 없습니다. 대량 로드에서는 데이터베이스가 올바로 설정되어 있고 사용자 컨텍스트(즉, 대량 로드에 사용하도록 설정된 로그인)에 적절한 사용 권한이 설정되어 있다고 가정합니다.  
  
-   비트랜잭션 모드에서 대량 로드 프로세스 중에 오류가 발생하면 데이터가 부분 로드된 상태로 남아 있을 수 있습니다. 이 오류가 발생하는 시점에 해당 위치에서 대량 로드가 중지됩니다. 트랜잭션 모드를 사용하면 이 문제를 완화할 수 있습니다.  
  
-   대량 로드 오류가 발생할 때 오류 정보에 데이터베이스에 대한 정보가 포함될 수 있습니다. 예를 들어 테이블이나 열 이름 또는 열 형식 정보가 포함될 수 있습니다. 대량 로드를 사용할 때는 오류를 사용자에게 직접 노출하기 보다는 대량 로드 프로세스에서 오류를 catch하고 일반 오류 메시지를 반환하도록 해야 합니다.  
  
-   대량 로드 작업에서 처리할 수 있는 데이터 양에는 제한이 없습니다. 대량 로드에서는 로드할 데이터의 크기를 확인하지 않습니다. 대량 로드 작업을 실행할 때 지정한 파일을 처리하는 데 필요한 메모리가 충분한지, 그리고 로드하는 데이터를 저장할 공간이 데이터베이스에 있는지는 사용자가 확인해야 합니다.  
  
-   대량 로드에서는 코드로 지정된 데이터를 사용하지 않습니다. 또한 데이터 입력을 어떠한 방식으로든 실행하지 않습니다. 입력 데이터의 모든 코드나 명령은 일반 데이터로 처리되며 실행되지 않습니다.  
  
-   대량 로드에서는 XML과 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터 모델 간의 차이를 기준으로 지정된 데이터의 형식을 변경할 수 있습니다. 예를 들어 시간을 지정하는 형식이 다를 경우 대량 로드에서 이러한 차이를 해결하려고 합니다. 따라서 일부 전체 자릿수 정보가 손실될 수 있습니다.  
  
-   대량 로드에서는 데이터를 처리하는 데 걸리는 시간에 제한이 없습니다. 처리가 완료되거나 오류가 발생할 때까지 처리 작업이 계속됩니다.  
  
-   대량 로드에서는 데이터베이스 내에서 임시 테이블을 만들거나 삭제할 수 있으므로 이 작업을 위한 권한이 필요합니다. 이러한 테이블에 대한 사용 권한은 대량 로드 프로세스를 위해 데이터베이스에 연결하고 있는 동일한 사용자에게 부여됩니다.  
  
-   대량 로드에서는 트랜잭션 모드 처리 동안 사용되는 임시 파일을 만들거나 삭제할 수 있으므로 이 작업을 위한 권한이 필요합니다. 이러한 파일은 대량 로드가 실행되고 있는 스레드의 현재 사용자와 동일한 사용 권한으로 만들어집니다.  
  
-   사용자가 SQLXML에서 오류를 기록할 오류 로그 파일을 설정하는 경우 대량 로드를 실행할 때마다 이 파일이 마지막 대량 로드 프로세스의 데이터로 덮어쓰여집니다.  
  
## <a name="see-also"></a>참고 항목  
 [XML 데이터 대량 로드 수행&#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/bulk-load-xml/performing-bulk-load-of-xml-data-sqlxml-4-0.md)  
  
  
