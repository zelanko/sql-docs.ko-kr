---
title: 상시 암호화로 보호되는 중요한 데이터 마이그레이션 | Microsoft 문서
ms.custom: ''
ms.date: 11/04/2015
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: vanto
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Always Encrypted, bulk import
ms.assetid: b2ca08ed-a927-40fb-9059-09496752595e
author: aliceku
ms.author: aliceku
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: ebe1af350632325d56fdf0251b790082fb443e97
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47769241"
---
# <a name="migrate-sensitive-data-protected-by-always-encrypted"></a>상시 암호화로 보호되는 중요한 데이터 마이그레이션
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
 대량 복사 작업 중 서버에서 메타데이터 검사를 수행하지 않고 암호화된 데이터를 로드하려면 **ALLOW_ENCRYPTED_VALUE_MODIFICATIONS** 옵션으로 사용자를 만듭니다. 이 옵션은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 이전 [!INCLUDE[ssSQL15](../../../includes/sssql15-md.md)] 버전의 레거시 도구(예: bcp.exe) 또는 상시 암호화를 사용할 수 없는 타사 ETL(추출-변환-로드) 워크플로를 통해 사용하기 위한 것입니다. 이를 통해 사용자는 암호화된 데이터를 암호화된 열이 포함된 하나의 테이블 집합에서 암호화된 열이 있는 다른 테이블 집합(같거나 다른 데이터베이스)으로 안전하게 이동할 수 있습니다.  
 -  
 ## <a name="the-allowencryptedvaluemodifications-option"></a>The ALLOW_ENCRYPTED_VALUE_MODIFICATIONS 옵션  
 [CREATE USER](../../../t-sql/statements/create-user-transact-sql.md) 와 [ALTER USER](../../../t-sql/statements/alter-user-transact-sql.md) 둘 다 ALLOW_ENCRYPTED_VALUE_MODIFICATIONS 옵션이 있습니다. ON으로 설정되어 있는 경우(기본값은 OFF) 이 옵션은 대량 복사 작업에서 서버에 대한 암호화 메타데이터 검사를 억제하여 사용자는 데이터를 암호 해독하지 않고 테이블 또는 데이터베이스 간에 암호화된 데이터를 대량 복사할 수 있습니다.  
  
## <a name="data-migration-scenarios"></a>데이터 마이그레이션 시나리오  
다음 표는 몇 가지 마이그레이션 시나리오에 적합한 권장된 설정을 보여줍니다.  
 
![always-encrypted-migration](../../../relational-databases/security/encryption/media/always-encrypted-migration.PNG "always-encrypted-migration")  

## <a name="bulk-loading-of-encrypted-data"></a>암호화된 데이터의 대량 로드  
다음 프로세스를 사용하여 암호화된 데이터를 로드합니다.  

1.  데이터베이스에서 대량 복사 작업 대상인 사용자에 대해 이 옵션을 ON으로 설정합니다. 예를 들어 다음과 같이 사용할 수 있습니다.  
 
   ```  
    ALTER USER Bob WITH ALLOW_ENCRYPTED_VALUE_MODIFICATIONS = ON;  
   ```  

2.  해당 사용자로 연결하는 대량 복사 애플리케이션 또는 도구를 실행합니다. (애플리케이션에서 상시 암호화가 사용 설정된 클라이언트 드라이버를 사용하고 있는 경우 암호화된 열에서 검색된 데이터가 암호화를 유지하도록 데이터 원본에 대한 연결 문자열에 **column encryption setting=enabled** 가 포함되지 않아야 합니다. 자세한 내용은 [상시 암호화&#40;클라이언트 개발&#41;](../../../relational-databases/security/encryption/always-encrypted-client-development.md)를 참조하세요.  
  
3.  ALLOW_ENCRYPTED_VALUE_MODIFICATIONS 옵션을 다시 OFF로 설정합니다. 예를 들어 다음과 같이 사용할 수 있습니다.  

    ```  
    ALTER USER Bob WITH ALLOW_ENCRYPTED_VALUE_MODIFICATIONS = OFF;  
    ```  

## <a name="potential-for-data-corruption"></a>데이터 손상 가능성  
이 옵션을 부적절하게 사용할 경우 데이터가 손상될 수 있습니다. **ALLOW_ENCRYPTED_VALUE_MODIFICATIONS** 옵션을 통해 사용자는 다른 키, 잘못 암호화 또는 전혀 암호화되지 않은 데이터를 포함해 모든 데이터를 데이터베이스의 암호화된 열로 삽입할 수 있습니다. 사용자가 대상 열에 대해 설저된 암호화 구성표(열 암호화 키, 알고리즘, 암호화 유형)를 사용하여 올바르게 암호화되지 않은 데이터를 실수로 복사하는 경우 데이터를 해독할 수 없습니다(데이터가 손상됨). 데이터베이스의 데이터를 손상시킬 수 있으므로, 이 옵션은 신중하게 사용해야 합니다.  

다음 시나리오는 데이터를 부적절하게 가져올 경우 어떻게 데이터가 손상될 수 있는지 보여줍니다.  

1.  옵션은 사용자에 대해 ON으로 설정되어 있습니다.  
 
2.  사용자는 데이터베이스에 연결하는 애플리케이션을 실행합니다. 애플리케이션은 대량 API를 사용하여 일반 텍스트 값을 암호화된 열에 삽입합니다. 애플리케이션은 상시 암호화가 사용 설정된 클라이언트 드라이버가 삽입 시 데이터를 암호할 것을 예상합니다. 그러나 애플리케이션이 잘못 구성되어 있으므로, 상시 암호화를 지원하지 않는 드라이버 사용을 종료하거나 연결 문자열에 **column encryption setting=enabled**가 포함되지 않습니다.  

3.  애플리케이션은 서버에 일반 텍스트 값을 보냅니다. 암호화 메타데이터 검사가 사용자에 대해 서버에서 사용하지 않도록 설정되어 있으므로, 서버는 잘못된 데이터(올바르게 암호화된 암호 텍스트 대신 일반 텍스트)를 암호화된 열로 삽입하게 됩니다.  
 
4.  같거나 다른 애플리케이션이 상시 암호화 사용 설정된 드라이버를 사용하고 연결 문자열에서 **column encryption setting=enabled** 상태로 데이터베이스에 연결하며 데이터를 검색합니다. 애플리케이션은 데이터가 투명하게 암호 해독될 것을 예상합니다. 그러나 데이터가 잘못된 암호 텍스트이므로 데이터의 암호를 해독하지 못합니다.  

## <a name="best-practice"></a>최선의 구현 방법  
 
이 옵션을 사용하여 장기 실행 작업에 지정된 사용자 계정을 사용합니다.  
 
해독하지 않고 암호화된 데이터를 이동해야 하는 단기 실행 대량 복사 애플리케이션 또는 도구의 경우 애플리케이션을 실행하기 직전에 이 옵션을 ON으로 설정하고 작업을 실행한 직후에 다시 OFF로 설정합니다.  
 
새 애플리케이션 개발에 이 옵션을 사용하지 말고 대신 단일 세션에 대한 암호화 메타데이터 검사 억제에 API를 제공하는 클라이언트 드라이버(예: ADO 4.6.1)를 사용하세요.  

## <a name="see-also"></a>참고 항목  
[CREATE USER&#40;Transact-SQL&#41;](../../../t-sql/statements/create-user-transact-sql.md)   
[ALTER USER&#40;Transact-SQL&#41;](../../../t-sql/statements/alter-user-transact-sql.md)   
[상시 암호화&#40;데이터베이스 엔진&#41;](../../../relational-databases/security/encryption/always-encrypted-database-engine.md)   
[상시 암호화 마법사](../../../relational-databases/security/encryption/always-encrypted-wizard.md)   
[상시 암호화&#40;클라이언트 개발&#41;](../../../relational-databases/security/encryption/always-encrypted-client-development.md)  
