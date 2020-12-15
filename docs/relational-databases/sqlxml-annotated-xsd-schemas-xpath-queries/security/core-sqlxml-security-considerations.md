---
title: 핵심 SQLXML 보안 고려 사항
description: 데이터 액세스에 SQLXML을 사용 하기 위한 핵심 보안 지침에 대해 알아봅니다.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- security [SQLXML], about security
ms.assetid: 330cd2ff-d5d5-4c8e-8f93-0869c977be94
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 477124bc7dac925e48fc1a31382197daefefa4f7
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97439608"
---
# <a name="core-sqlxml-security-considerations"></a>핵심 SQLXML 보안 고려 사항
[!INCLUDE [SQL Server Azure SQL Database](../../../includes/applies-to-version/sql-asdb.md)]
  다음은 데이터 액세스에 SQLXML을 사용하는 경우에 대한 보안 지침입니다.  
  
-   SQLXMLOLEDB 공급자는 각 특정 인스턴스에 대해 사용 하거나 사용 하지 않도록 설정할 SQLXML 기능을 나타내는 플래그를 설정 하는 데 사용할 수 있는 **streamflags** 속성을 노출 합니다. 이 속성을 사용하여 SQLXML 사용을 사용자 지정하고 원하는 구성 요소만 사용되도록 설정할 수 있습니다. 자세한 내용은 [SQLXMLOLEDB Provider &#40;SQLXML 4.0&#41;](../data-access-components-provider/sqlxml-4-0-data-access-components-sqlxmloledb-provider.md)를 참조 하세요.  
  
-   SQLXML 오류가 발생하고 반환되는 경우 테이블 이름, 열 이름 또는 유형 정보와 같은 데이터베이스 스키마 정보가 포함될 수 있습니다. 의도되지 않았거나 필요하지 않은 경우 사용자가 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 설치에 대한 정보를 쉽게 검색할 수 없도록 이러한 오류를 처리할 때는 주의해야 합니다.  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]를 쿼리하거나 업데이트를 보내기 위해 사용하는 경우 SQLXML은 교환할 수 있는 데이터 양에 제한을 설정하지 않으며, 처리 전에 SQLXML 페이로드의 데이터 크기를 확인하지도 않습니다. SQLXML을 사용하여 애플리케이션을 개발하는 경우 시스템에 데이터를 처리할 충분한 메모리가 있는지 확인해야 합니다. 예를 들어 서버의 데이터를 쿼리하는 경우 클라이언트 메모리에 해당 데이터를 받아들일 충분한 공간이 있는지 확인해야 합니다. 마찬가지로, 데이터를 서버로 로드하는 경우 해당 데이터를 처리하는 데 필요한 메모리를 서버에서 사용할 수 있는지, 그리고 서버에서 사용 가능한 디스크 저장 공간이 데이터를 저장하기에 충분한지 확인해야 합니다.  
  
-   SQLXML은 동적으로 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 쿼리 및 업데이트 명령을 생성하여 실행을 위해 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]로 보냅니다. SQLXML은 이런 방식으로만 서버를 쿼리하고 업데이트할 수 있습니다. 결과는 XML 스트림이나 행 집합으로 수신됩니다.  
  
-   쿼리 결과를 받을 때 SQLXML은 수신된 데이터의 내용을 기반으로 어떠한 동작도 수행하지 않습니다. 데이터 형식이나 내용을 기반으로 추가 처리가 수행되지 않습니다. 데이터는 동작을 실행할 코드로 처리되지 않습니다.  
  
-   XML 템플릿을 실행하는 경우 SQLXML은 제출된 템플릿 내에 포함된 XPath 및 DBObject 쿼리를 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 명령으로 변환합니다. 이 명령은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에 대해 실행됩니다. 이 명령은 기존 데이터에만 적용됩니다. SQLXML에서 생성된 명령은 데이터베이스 구조를 변경하지 않습니다. 데이터베이스 구조를 변경하려면 사용자는 명시적인 명령을 실행해야 합니다. 예를 들어, 템플릿의 **sql: 쿼리** 블록에 포함 합니다.  
  
-   매핑 파일을 통해 DBObject 쿼리와 XPath 문을 실행하는 경우 SQLXML은 어떤 방식으로든 데이터베이스의 데이터를 변경하지 않습니다.  
  
-   SQLXML에서 XML과 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터 모델 사이의 차이를 기반으로 지정된 데이터 형식을 변경할 수 있습니다. 예를 들어 시간을 지정하는 형식이 다를 경우 SQLXML에서 이러한 차이를 해결하려고 합니다. 따라서 일부 전체 자릿수 정보가 손실될 수 있습니다.  
  
-   SQLXML은 데이터를 처리하는 데 걸리는 시간에 제한을 설정하지 않습니다. 오류가 발생하거나 처리가 완료될 때까지 처리 작업이 계속됩니다.  
  
-   SQLXML은 파일 시스템에 쓰지 않습니다. 사용자가 데이터베이스에서 검색한 데이터를 저장하려는 경우 해당 코드에서 이 작업을 수행해야 합니다.  
  
-   SQLXML을 통해 사용자는 원하는 모든 SQL 쿼리를 데이터베이스에 대해 실행할 수 있습니다. 보안되지 않은 원본이나 제어되지 않은 원본에는 이 기능을 노출하면 안 됩니다. 그렇지 않으면 프로비전 없이 SQL 데이터베이스가 모든 사용자에게 열리게 됩니다.  
  
-   Updategrams을 실행할 때 SQLXML은 **updg: sync** 블록을 인스턴스에 대해 DELETE, UPDATE 및 INSERT 명령으로 변환 합니다 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . 이 명령은 기존 데이터에만 적용됩니다. SQLXML에서 생성된 명령은 데이터베이스를 변경하지 않습니다. 데이터베이스 구조를 변경하려면 사용자는 명시적인 명령을 실행해야 합니다. 예를 들어, 템플릿의 **sql: 쿼리** 블록에 포함 합니다.  
  
-   DiffGram을 실행하는 경우 SQLXML은 DiffGram을 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스에 대한 DELETE, UPDATE 및 INSERT 명령으로 변환합니다. 이 명령은 기존 데이터에만 적용됩니다. SQLXML에서 생성된 명령은 데이터베이스를 변경하지 않습니다. 데이터베이스 구조를 변경하려면 사용자는 명시적인 명령을 실행해야 합니다. 예를 들어, 템플릿의 **sql: 쿼리** 블록에 포함 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLXML 4.0 보안 고려 사항](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/security/sqlxml-4-0-security-considerations.md)  
  
