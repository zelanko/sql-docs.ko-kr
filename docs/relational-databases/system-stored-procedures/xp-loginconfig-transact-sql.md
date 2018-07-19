---
title: xp_loginconfig (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- xp_loginconfig_TSQL
- xp_loginconfig
dev_langs:
- TSQL
helpviewer_keywords:
- xp_loginconfig
ms.assetid: d380e799-2857-408a-bcbf-5e73a8e6aa5a
caps.latest.revision: 38
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 950a01041db936c83a5a3c799f1055ab3996aa34
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2018
ms.locfileid: "38003175"
---
# <a name="xploginconfig-transact-sql"></a>xp_loginconfig(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 로그인 보안 구성을 보고합니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
xp_loginconfig ['config_name']  
```  
  
## <a name="arguments"></a>인수  
 **'** *config_name* **'**  
 표시할 구성 값입니다. 하는 경우 *config_name* 은 지정 하지 않으면 모든 구성 값은 보고 됩니다. *config_name* 됩니다 **sysname**, 기본값은 NULL 이며 다음이 값 중 하나일 수 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**로그인 모드**|로그인 보안 모드입니다. 가능한 값은 **Mixed** 하 고 **Windows 인증**합니다.<br /><br /> 다음으로 대체됩니다.<br /><br /> `SELECT SERVERPROPERTY('IsIntegratedSecurityOnly'); GO`|  
|**기본 로그인**|일치하는 로그인 이름이 없는 사용자에 대해 트러스트된 연결의 권한이 있는 사용자에 대한 기본 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인 ID의 이름입니다. 기본 로그인은 **게스트**합니다. 이 값은 이전 버전과의 호환성을 위해 제공됩니다.|  
|**기본 도메인**|트러스트된 연결의 네트워크 사용자에 대한 기본 Windows 도메인 이름입니다. 기본 도메인은 Windows 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 실행하고 있는 컴퓨터의 도메인입니다. 이 값은 이전 버전과의 호환성을 위해 제공됩니다.|  
|**감사 수준**|감사 수준입니다. 가능한 값은 **없음**, **성공**, **장애**, 및 **모든**. 감사는 오류 로그 및 Windows 이벤트 뷰어에 기록됩니다.|  
|**호스트 이름 설정**|클라이언트 로그인 레코드의 호스트 이름이 Windows 네트워크 사용자 이름으로 대체되는지 여부를 나타냅니다. 가능한 값은 **true** 하거나 **false**합니다. 네트워크 사용자 이름에서 출력에 표시 되는이 값으로 설정 하는 경우 **sp_who**합니다.|  
|**지도 _**|유효한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 밑줄(_)에 매핑되는 Windows 특수 문자를 보고합니다. 가능한 값은 **도메인 구분 기호** (기본값) 이면 **공간**합니다 **null**, 또는 모든 단일 문자입니다. 이 값은 이전 버전과의 호환성을 위해 제공됩니다.|  
|**$ 매핑**|유효한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 달러 표시($)에 매핑되는 Windows 특수 문자를 보고합니다. 가능한 값은 **도메인 구분 기호**를 **공간**합니다 **null**, 또는 모든 단일 문자입니다. 기본값은 **공간**입니다. 이 값은 이전 버전과의 호환성을 위해 제공됩니다.|  
|**# 매핑**|유효한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 숫자 기호(#)에 매핑되는 Windows 특수 문자를 보고합니다. 가능한 값은 **도메인 구분 기호**를 **공간**합니다 **null**, 또는 모든 단일 문자입니다. 기본값은 하이픈입니다. 이 값은 이전 버전과의 호환성을 위해 제공됩니다.|  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="result-sets"></a>결과 집합  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|구성 값|  
|**구성 값**|**sysname**|구성 값 설정|  
  
## <a name="remarks"></a>Remarks  
 **xp_loginconfig** 구성 값 설정에 사용할 수 없습니다.  
  
 로그인 모드와 감사 수준을 설정하려면 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]를 사용합니다.  
  
## <a name="permissions"></a>사용 권한  
 에 대 한 CONTROL 권한이 필요 합니다 **마스터** 데이터베이스입니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-how-to-report-all-configuration-values"></a>1. 모든 구성 값을 보고하는 방법  
 다음 예에서는 현재 구성된 모든 설정을 표시합니다.  
  
```  
EXEC xp_loginconfig;  
GO  
```  
  
### <a name="b-how-to-report-a-specific-configuration-value"></a>2. 특정 구성 값을 보고하는 방법  
 다음 예에서는 로그인 모드에 관한 설정만을 표시합니다.  
  
```  
EXEC xp_loginconfig 'login mode';  
GO  
```  
  
## <a name="see-also"></a>관련 항목  
 [sp_denylogin&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-denylogin-transact-sql.md)   
 [sp_grantlogin&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-grantlogin-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [sp_revokelogin&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-revokelogin-transact-sql.md)   
 [xp_logininfo &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/xp-logininfo-transact-sql.md)  
  
  
