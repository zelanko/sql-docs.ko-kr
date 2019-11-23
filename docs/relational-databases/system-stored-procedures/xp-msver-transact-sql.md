---
title: xp_msver (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- xp_msver_TSQL
- xp_msver
dev_langs:
- TSQL
helpviewer_keywords:
- xp_msver
ms.assetid: 9264cf8c-92ba-45ad-b2d6-15d26d805a16
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 85552daa2dda14c6a7516c96f0f9fe6566f31111
ms.sourcegitcommit: f688a37bb6deac2e5b7730344165bbe2c57f9b9c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/08/2019
ms.locfileid: "73843896"
---
# <a name="xp_msver-transact-sql"></a>xp_msver(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 대한 버전 정보를 반환합니다. 서버에 대 한 실제 빌드 번호 및 서버 환경에 대 한 정보를 반환 하는 **xp_msver** 도 반환 합니다. **Xp_msver** 반환 되는 정보는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문, 일괄 처리, 저장 프로시저 등에서 사용 하 여 플랫폼 독립적인 코드의 논리를 향상 시킬 수 있습니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
xp_msver [ optname ]  
```  
  
## <a name="arguments"></a>인수  
 *optname*  
 옵션의 이름이며 다음 값 중 하나를 사용할 수 있습니다.  
  
|옵션/열 이름|설명|  
|-------------------------|-----------------|  
|**ProductName**|제품 이름; 예를 들어 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다.|  
|**ProductVersion**|제품 버전입니다.|  
|**언어**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 언어 버전입니다.|  
|**플랫폼**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 실행하는 컴퓨터의 운영 체제 이름, 제조업체 이름 및 칩 패밀리 이름입니다.|  
|**설명**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 대한 기타 정보입니다.|  
|**CompanyName**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 생산한 회사 이름입니다. 예를 들어 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Corporation 등입니다.|  
|**FileDescription**|운영 체제입니다.|  
|**FileVersion**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 실행 파일의 버전입니다.|  
|**InternalName**|[!INCLUDE[msCoName](../../includes/msconame-md.md)]에 대한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 내부 이름입니다. 예를 들어 SQLSERVR 등이 있습니다.|  
|**LegalCopyright**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 필요한 법률적 저작권 정보입니다. 예를 들어 Copyright© [!INCLUDE[msCoName](../../includes/msconame-md.md)] Corp. 1988-2005 등입니다.|  
|**LegalTrademarks**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 필요한 법률적 상표 정보입니다. 예를 들어 [!INCLUDE[msCoName](../../includes/msconame-md.md)]는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Corporation의 등록 상표입니다.|  
|**OriginalFilename**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 시작 시 실행되는 파일 이름입니다. 예를 들어 Sqlservr.exe 등입니다.|  
|**PrivateBuild**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**SpecialBuild**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**WindowsVersion**|[!INCLUDE[msCoName](../../includes/msconame-md.md)]를 실행하고 있는 컴퓨터에 설치된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Windows 버전입니다.|  
|**ProcessorCount**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 실행하고 있는 컴퓨터의 프로세서의 수입니다.|  
|**ProcessorActiveMask**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 실행하고 있는 컴퓨터에 설치된 프로세서 중 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows에서 시작되어 사용 가능한 프로세서를 나타냅니다.|  
|**ProcessorType**|프로세서 유형입니다. **플랫폼과**유사 합니다.|  
|**실제 메모리**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 실행하고 있는 컴퓨터에 설치된 RAM의 크기(MB)입니다.|  
|**제품 ID**|PID(제품 ID) 번호입니다. 이 번호는 설치 중에 지정되며 원본 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] CD 케이스의 스티커에 나와 있습니다.|  
  
## <a name="return-code-values"></a>반환 코드 값  
 1 (성공)  
  
## <a name="result-sets"></a>결과 집합  
 매개 변수 없이 **xp_msver**는 모든 옵션 값을 나열 하는 네 개의 열로 된 결과 집합을 반환 합니다. **xp_msver**매개 변수의 경우 해당 옵션 값이 포함 된 네 개의 열로 된 결과 집합을 반환 합니다.  
  
## <a name="permissions"></a>사용 권한  
 **public** 역할의 멤버 자격이 필요합니다.  
  
## <a name="see-also"></a>참고 항목  
 [시스템 함수&#40;Transact-SQL&#41;](../../relational-databases/system-functions/system-functions-category-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [일반 확장 저장 프로시저 &#40;transact-sql&#41; ](../../relational-databases/system-stored-procedures/general-extended-stored-procedures-transact-sql.md)   
 [@@VERSION&#40;Transact-SQL&#41;](../../t-sql/functions/version-transact-sql-configuration-functions.md)  
  
  
