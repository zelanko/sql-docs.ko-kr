---
title: 상시 암호화되는 암호화 | Microsoft 문서
ms.custom: ''
ms.date: 02/29/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: security
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Always Encrypted, cryptography system
ms.assetid: ae8226ff-0853-4716-be7b-673ce77dd370
caps.latest.revision: 11
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 578cbf195244f561fd65a14d40482103a59a72ca
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="always-encrypted-cryptography"></a>상시 암호화되는 암호화
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  이 문서에서는 [및](../../../relational-databases/security/encryption/always-encrypted-database-engine.md) 의 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 상시 암호화 [!INCLUDE[ssSDSFull](../../../includes/sssdsfull-md.md)]기능에서 사용되는 암호화 관련 자료를 유도하기 위한 암호화 알고리즘 및 메커니즘을 설명합니다.  
  
## <a name="keys-key-stores-and-key-encryption-algorithms"></a>키, 키 저장소 및 키 암호화 알고리즘  
 상시 암호화는 열 마스터 키 및 열 암호화 키의 두 가지 키 유형을 사용합니다.  
  
 열 마스터 키(CMK)는 항상 클라이언트가 관리하고 외부 키 저장소에 저장되는 키 암호화 키(예: 다른 키를 암호화하기 위해 사용되는 키)입니다. 상시 암호화 활성화 클라이언트 드라이버는 CMK 저장소 공급자를 통해 키 저장소와 상호작용하고 드라이버 라이브러리( [!INCLUDE[msCoName](../../../includes/msconame-md.md)]/시스템 공급자)의 일부 또는 클라이언트 응용 프로그램(사용자 지정 공급자)의 일부가 될 수 있습니다. 클라이언트 드라이버 라이브러리에는 현재 [Windows 인증서 저장소](https://msdn.microsoft.com/library/windows/desktop/aa388160) 및 하드웨어 보안 모듈(HSM)용 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] 키 저장소 공급자에 포함됩니다.  공급자의 현재 목록은 [CREATE COLUMN MASTER KEY&#40;Transact-SQL&#41;](../../../t-sql/statements/create-column-master-key-transact-sql.md)를 참조하세요. 응용 프로그램 개발자는 임의 저장소에 대한 사용자 지정 공급자를 제공할 수 있습니다.  
  
 열 암호화 키(CEK)는 CMK로 보호되는 콘텐츠 암호화 키(예: 데이터를 보호하기 위해 사용되는 키)입니다.  
  
 모든 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] CMK 저장소 공급자는 RFC 3447 섹션 2.1항에 의해 지정된 기본 매개 변수가 있는 최적 비대칭 암호화 패딩(RSA-OAEP)와 RSA를 사용하여 CEK를 암호화합니다. 이러한 기본 매개 변수는 SHA-1의 해시 기능과 SHA-1가 있는 MGF1의 마스크 생성 기능을 사용합니다.  
  
## <a name="data-encryption-algorithm"></a>데이터 암호화 알고리즘  
 상시 암호화는 **AEAD_AES_256_CBC_HMAC_SHA_256** 알고리즘을 사용하여 데이터베이스에서 데이터를 암호화합니다.  
  
 **AEAD_AES_256_CBC_HMAC_SHA_256**은 [http://tools.ietf.org/html/draft-mcgrew-aead-aes-cbc-hmac-sha2-05](http://tools.ietf.org/html/draft-mcgrew-aead-aes-cbc-hmac-sha2-05)의 사양 초안에서 파생되었습니다. 관련 데이터와 인증 암호화 체계를 사용하며 암호화 후 MAC 방식을 따릅니다. 즉, 일반 텍스트를 먼저 암호화한 후 결과 암호 텍스트에 따라 MAC이 생성됩니다.  
  
 패턴을 숨기기 위해 **AEAD_AES_256_CBC_HMAC_SHA_256** 은 작업의 CBC(암호화 블록 체인) 모드를 사용하고 여기에서 초기 값은 초기화 벡터(IV)라는 이름으로 시스템에 제공됩니다. CBC 모드에 대한 자세한 설명은 [http://csrc.nist.gov/publications/nistpubs/800-38a/sp800-38a.pdf](http://csrc.nist.gov/publications/nistpubs/800-38a/sp800-38a.pdf)에 있습니다.  
  
 **AEAD_AES_256_CBC_HMAC_SHA_256** 은 다음 단계를 통해 지정된 일반 텍스트 값에 대한 암호화 값을 계산합니다.  
  
### <a name="step-1-generating-the-initialization-vector-iv"></a>1단계: 초기화 벡터(IV) 생성  
 상시 암호화가 지원하는 **AEAD_AES_256_CBC_HMAC_SHA_256**의 두 가지 유형:  
  
-   임의  
  
-   결정적  
  
 임의 암호화의 경우 IV가 임의로 생성됩니다. 결과적으로 동일한 일반 텍스트가 암호화될 때마다 서로 다른 암호 텍스트가 생성되고 이를 통해 모든 정보가 공개되는 것이 방지됩니다.  
  
```  
When using randomized encryption: IV = Generate cryptographicaly random 128bits  
```  
  
 결정적 암호화의 경우 IV가 임의로 생성되지 않고 다음 알고리즘을 사용하여 일반 텍스트 값에서 유도됩니다.  
  
```  
When using deterministic encryption: IV = HMAC-SHA-256( iv_key, cell_data ) truncated to 128 bits.  
```  
  
 여기서 iv_key는 다음 방식으로 CEK에서 유도됩니다.  
  
```  
iv_key = HMAC-SHA-256(CEK, "Microsoft SQL Server cell IV key" + algorithm + CEK_length)  
```  
  
 필요한 경우 IV에서는 데이터 1블록에 맞추기 위해 HMAC 값 잘림이 수행됩니다.    
결과적으로, 결정적 암호화는 지정된 일반 텍스트 값에 대하여 동일한 암호 텍스트를 생성하여 상응하는 암호 텍스트 값을 비교함으로써 두 일반 텍스트 값이 동일한지 유추할 수 있습니다. 이러한 제한된 정보 공개를 통해 데이터베이스 시스템은 암호화 열 값에서 동등 비교를 지원할 수 있습니다.  
  
 다른 방식과 비교했을 때 결정적 암호화는 미리 정의된 IV 값을 사용하는 것과 같이 패턴 숨기기에서 더 효과적입니다.  
  
### <a name="step-2-computing-aes256cbc-ciphertext"></a>2단계: AES_256_CBC 암호 텍스트 계산  
 IV를 계산한 후 **AES_256_CBC** 암호 텍스트가 생성됩니다.  
  
```  
aes_256_cbc_ciphertext = AES-CBC-256(enc_key, IV, cell_data) with PKCS7 padding.  
```  
  
 여기에서 암호화 키(enc_key)는 다음과 같이 CEK에서 파생됩니다.  
  
```  
enc_key = HMAC-SHA-256(CEK, "Microsoft SQL Server cell encryption key" + algorithm + CEK_length )  
```  
  
### <a name="step-3-computing-mac"></a>3단계: MAC 계산  
 그 후 다음 알고리즘을 사용하여 MAC이 계산됩니다.  
  
```  
MAC = HMAC-SHA-256(mac_key, versionbyte + IV + Ciphertext + versionbyte_length)  
```  
  
 각 항목이 나타내는 의미는 다음과 같습니다.  
  
```  
versionbyte = 0x01 and versionbyte_length = 1   
mac_key = HMAC-SHA-256(CEK, "Microsoft SQL Server cell MAC key" + algorithm + CEK_length)  
```  
  
### <a name="step-4-concatenation"></a>4단계: 연결  
 마지막으로, 알고리즘 버전 바이트, MAC, IV 및 AES_256_CBC 암호 텍스트를 단순히 연결하여 암호화된 값이 생성됩니다.  
  
```  
aead_aes_256_cbc_hmac_sha_256 = versionbyte + MAC + IV + aes_256_cbc_ciphertext  
```  
  
## <a name="ciphertext-length"></a>암호 텍스트 길이  
 **AEAD_AES_256_CBC_HMAC_SHA_256** 암호 텍스트 특정 컴포넌트의 길이(바이트 단위)는 다음과 같습니다.  
  
-   버전 바이트: 1  
  
-   MAC: 32  
  
-   IV: 16  
  
-   aes_256_cbc_ciphertext: `(FLOOR (DATALENGTH(cell_data)/ block_size) + 1)* block_size`, 여기에서:  
  
    -   block_size는 16바이트입니다.  
  
    -   cell_data은 일반 텍스트 값입니다.  
  
     따라서 aes_256_cbc_ciphertext의 최소 크기는 1블록(16바이트)입니다.  
  
 따라서 지정된 일반 텍스트 값(cell_data)을 암호화하여 생성된 암호 텍스트 길이는 다음 수식을 사용하여 계산될 수 있습니다.  
  
```  
1 + 32 + 16 + (FLOOR(DATALENGTH(cell_data)/16) + 1) * 16  
```  
  
 예를 들어 다음과 같이 사용할 수 있습니다.  
  
-   4바이트 길이 **int** 일반 텍스트 값은 암호화 후 65바이트 길이의 이진 값이 됩니다.  
  
-   2,000바이트 길이 **nchar(1000)** 일반 텍스트 값은 암호화 후 2,065바이트 길이의 이진 값이 됩니다.  
  
 다음 표는 전체 데이터 유형 목록 및 각 유형의 암호화 텍스트 길이를 보여줍니다.  
  
|데이터 형식|암호 텍스트 길이[바이트]|  
|---------------|---------------------------------|  
|**bigint**|65|  
|**binary**|다양함 위의 수식을 사용합니다.|  
|**bit**|65|  
|**char**|다양함 위의 수식을 사용합니다.|  
|**date**|65|  
|**datetime**|65|  
|**datetime2**|65|  
|**datetimeoffset**|65|  
|**decimal**|81|  
|**float**|65|  
|**geography**|해당 없음(지원되지 않음)|  
|**geometry**|해당 없음(지원되지 않음)|  
|**hierarchyid**|해당 없음(지원되지 않음)|  
|**image**|해당 없음(지원되지 않음)|  
|**int**|65|  
|**money**|65|  
|**nchar**|다양함 위의 수식을 사용합니다.|  
|**ntext**|해당 없음(지원되지 않음)|  
|**numeric**|81|  
|**nvarchar**|다양함 위의 수식을 사용합니다.|  
|**real**|65|  
|**smalldatetime**|65|  
|**smallint**|65|  
|**smallmoney**|65|  
|**sql_variant**|해당 없음(지원되지 않음)|  
|**sysname**|해당 없음(지원되지 않음)|  
|**text**|해당 없음(지원되지 않음)|  
|**time**|65|  
|**timestamp**<br /><br /> (**rowversion**)|해당 없음(지원되지 않음)|  
|**tinyint**|65|  
|**uniqueidentifier**|81|  
|**varbinary**|다양함 위의 수식을 사용합니다.|  
|**varchar**|다양함 위의 수식을 사용합니다.|  
|**xml**|해당 없음(지원되지 않음)|  
  
## <a name="net-reference"></a>.NET 참조  
 이 문서에서 설명된 알고리즘에 대한 자세한 내용은 **.NET 참조** 에서 **SqlAeadAes256CbcHmac256Algorithm.cs** 및 [SqlColumnEncryptionCertificateStoreProvider.cs](http://referencesource.microsoft.com/)파일을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [상시 암호화&#40;데이터베이스 엔진&#41;](../../../relational-databases/security/encryption/always-encrypted-database-engine.md)   
 [상시 암호화&#40;클라이언트 개발&#41;](../../../relational-databases/security/encryption/always-encrypted-client-development.md)  
  
  
