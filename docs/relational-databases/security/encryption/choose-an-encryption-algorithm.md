---
title: 암호화 알고리즘 선택 | Microsoft 문서
ms.custom: ''
ms.date: 08/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: vanto
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- cryptography [SQL Server], algorithms
- encryption [SQL Server], algorithms
- security [SQL Server], encryption
- algorithms [SQL Server encryption]
ms.assetid: 8227028c-a9c9-489d-bd27-fbf8242634ae
author: jaszymas
ms.author: jaszymas
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: e73d0d6cdf244cfb9e08993c91737a14a1d2b24b
ms.sourcegitcommit: 39ea690996a7390e3d13d6fb8f39d8641cd5f710
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/10/2019
ms.locfileid: "74957464"
---
# <a name="choose-an-encryption-algorithm"></a>암호화 알고리즘 선택
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  암호화는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]의 인터페이스를 보호하려는 관리자가 사용할 수 있는 여러 가지 심층 방어 중 하나입니다.  
  
 암호화 알고리즘은 권한이 없는 사용자가 쉽게 바꿀 수 없는 데이터 변환을 정의합니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 를 사용하면 관리자와 개발자가 DES, Triple DES, TRIPLE_DES_3KEY, RC2, RC4, 128비트 RC4, DESX, 128비트 AES, 192비트 AES, 256비트 AES 등의 여러 알고리즘 중에서 원하는 알고리즘을 선택할 수 있습니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssSQL15](../../../includes/sssql15-md.md)]부터는 AES_128, AES_192 및 AES_256 이외의 모든 알고리즘을 지원하지 않습니다. 오래된 알고리즘을 사용하려면(권장하지 않음) 데이터베이스 호환성 수준을 120 이하로 설정해야 합니다.  
  
 모든 상황에 맞는 이상적인 단일 알고리즘은 없으며 각 알고리즘의 장점에 대한 내용은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 온라인 설명서에서 다루지 않지만 다음과 같은 일반적인 원칙이 적용됩니다.  
  
-   강력한 암호화는 일반적으로 약한 암호화보다 더 많은 CPU 리소스를 사용합니다.  
  
-   일반적으로 짧은 키보다 긴 키가 강력한 암호화를 생성합니다.  
  
-   비대칭 암호화는 대칭 암호화보다 느립니다.  
  
-   짧은 암호보다 길고 복잡한 암호가 강력합니다.  

-   대칭 암호화는 일반적으로 키가 로컬에만 저장되어 있을 때 권장되며, 네트워크를 통해 키를 공유해야 할 때는 비대칭 암호화를 사용하는 것이 좋습니다.
  
-   많은 양의 데이터를 암호화하는 경우 대칭 키를 사용하여 데이터를 암호화한 다음 비대칭 키를 사용하여 해당 대칭 키를 암호화하는 것이 좋습니다.  
  
-   암호화된 데이터는 압축할 수 없지만 압축된 데이터는 암호화할 수 있습니다. 압축을 사용할 경우 데이터를 암호화하기 전에 먼저 압축해야 합니다.  
  
> [!IMPORTANT]  
>  RC4 알고리즘은 이전 버전과의 호환성을 위해서만 지원됩니다. 데이터베이스의 호환성 수준이 90 또는 100인 경우 새 자료는 RC4 또는 RC4_128로만 암호화할 수 있습니다. 이 옵션은 사용하지 않는 것이 좋습니다. 대신 AES 알고리즘 중 하나와 같은 새 알고리즘을 사용하십시오. [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] 이상에서 RC4 또는 RC4_128을 사용하여 암호화된 자료는 모든 호환성 수준에서 해독할 수 있습니다.  
>   
>  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 에서는 솔트를 자동으로 제공하지 않기 때문에 서로 다른 데이터 블록에서 동일한 RC4 또는 RC4_128 KEY_GUID를 반복해서 사용하면 동일한 RC4 키가 만들어집니다. 동일한 RC4 키를 반복해서 사용하는 것은 암호화를 매우 약하게 만드는 잘 알려진 오류입니다. 따라서 RC4 및 RC4_128 키워드는 더 이상 사용되지 않습니다. [!INCLUDE[ssNoteDepFutureDontUse](../../../includes/ssnotedepfuturedontuse-md.md)]  
  
 암호화 알고리즘 및 암호화 기술에 대한 자세한 내용은 MSDN에서 .NET Framework Developer's Guide의 [주요 보안 개념(Key Security Concepts)](https://go.microsoft.com/fwlink/?LinkId=62082) 을 참조하십시오.  
  
 **DES 알고리즘 관련 설명:**  
  
-   DESX 이름이 잘못 지정되었습니다. ALGORITHM = DESX를 사용하여 만든 대칭 키에 실제로 192비트 키를 포함하는 TRIPLE DES 암호화가 사용됩니다. DESX 알고리즘은 제공되지 않습니다. [!INCLUDE[ssNoteDepFutureAvoid](../../../includes/ssnotedepfutureavoid-md.md)]  
  
-   ALGORITHM = TRIPLE_DES_3KEY를 사용하여 만든 대칭 키에 192비트 키를 포함하는 TRIPLE DES가 사용됩니다.  
  
-   ALGORITHM = TRIPLE_DES를 사용하여 만든 대칭 키에 128비트 키를 포함하는 TRIPLE DES가 사용됩니다.  
  
## <a name="related-tasks"></a>관련 작업  
  
|||  
|-|-|  
|대칭 키를 사용하여 암호화|[CREATE SYMMETRIC KEY &#40;Transact-SQL&#41;](../../../t-sql/statements/create-symmetric-key-transact-sql.md)|  
|비대칭 키를 사용하여 암호화|[CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../../t-sql/statements/create-asymmetric-key-transact-sql.md)|  
|인증서를 사용하여 암호화|[CREATE CERTIFICATE&#40;Transact-SQL&#41;](../../../t-sql/statements/create-certificate-transact-sql.md)|  
|투명한 데이터 암호화를 사용하여 데이터베이스 파일 암호화|[투명한 데이터 암호화&#40;TDE&#41;](../../../relational-databases/security/encryption/transparent-data-encryption.md)|  
|테이블의 한 열을 암호화하는 방법|[데이터 열 암호화](../../../relational-databases/security/encryption/encrypt-a-column-of-data.md)|  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server 암호화](../../../relational-databases/security/encryption/sql-server-encryption.md)   
 [암호화 계층](../../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  
