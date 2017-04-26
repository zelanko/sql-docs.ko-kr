---
title: "MSSQLSERVER_33085 | Microsoft 문서"
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- 33085 (Database Engine error)
ms.assetid: c27b8d1d-668a-4ba8-8b61-25a5ebbc5485
caps.latest.revision: 9
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: a0a4c315a40a70084e1f97f5b3c52081356d4aa0
ms.lasthandoff: 04/11/2017

---
# <a name="mssqlserver33085"></a>MSSQLSERVER_33085
  
## <a name="details"></a>세부 정보  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|33085|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|SEC_CRYPTOPROVE_METHOD_CANNOT_FOUND|  
|메시지 텍스트|암호화 공급자 라이브러리 '%.*ls'에서 하나 이상의 메서드를 찾을 수 없습니다.|  
  
## <a name="explanation"></a>설명  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 위의 오류 메시지에 나열된 암호화 공급자를 사용할 수 없습니다. 암호화 공급자가 필요한 메서드를 지원하지 않았습니다. 오류의 상태는 찾지 못한 메서드를 나타냅니다.  
  
|State|Description|  
|---------|---------------|  
|1|SqlCryptInitializeProvider|  
|2|SqlCryptFreeProvider|  
|3|SqlCryptOpenSession|  
|4|SqlCryptCloseSession|  
|5|SqlCryptGetProviderInfo|  
|6|SqlCryptGetNextAlgorithmId|  
|7|SqlCryptGetAlgorithmInfo|  
|8|SqlCryptCreateKey|  
|9|SqlCryptDropKey|  
|10|SqlCryptGetNextKeyId|  
|11|SqlCryptGetKeyInfoByKeyId|  
|12|SqlCryptGetKeyInfoByThumb|  
|13|SqlCryptGetKeyInfoByName|  
|14|SqlCryptExportKey|  
|15|SqlCryptImportKey|  
|16|SqlCryptEncrypt|  
|17|SqlCryptDecrypt|  
  
## <a name="user-action"></a>사용자 동작  
암호화 공급자에게 자세한 정보를 문의합니다.  
  

