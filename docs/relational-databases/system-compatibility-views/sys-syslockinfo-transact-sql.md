---
title: sys.syslockinfo (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- syslockinfo_TSQL
- sys.syslockinfo_TSQL
- sys.syslockinfo
- syslockinfo
dev_langs:
- TSQL
helpviewer_keywords:
- syslockinfo system table
- sys.syslockinfo compatibility view
ms.assetid: d8cae434-807a-473e-b94f-f7a0e1b2daf0
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 29446f34777682ff98ef6ec7c438c72db58e7167
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47780881"
---
# <a name="syssyslockinfo-transact-sql"></a>sys.syslockinfo(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  모든 허가된 잠금, 변환 중인 잠금, 대기 중인 잠금 요청에 대한 정보를 포함합니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssnoteCompView](../../includes/ssnotecompview-md.md)]  
  
> [!IMPORTANT]  
>  이 기능은 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 변경되었습니다. 자세한 내용은 [SQL Server 2016 데이터베이스 엔진 기능의 주요 변경 내용](../../database-engine/breaking-changes-to-database-engine-features-in-sql-server-2016.md)합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**rsc_text**|**nchar(32)**|잠금 리소스에 관한 문자 설명입니다. 리소스 이름의 일부를 포함합니다.|  
|**rsc_bin**|**binary(16)**|이진 잠금 리소스입니다. 잠금 관리자에 있는 실제 잠금 리소스를 포함합니다. 알고 있는 도구를 생성 하기 위한 잠금 리소스 형식을 자체 형식의 잠금 리소스에 대 한이 열은 포함 되어 있으며 자체에서 조인을 수행 하는 데 **syslockinfo**합니다.|  
|**rsc_valblk**|**binary(16)**|잠금 값 블록입니다. 일부 리소스 유형은 잠금 관리자가 해시하지 않은 잠금 리소스에 추가 데이터를 포함하여 특정 잠금 리소스의 소유권을 결정할 수 있습니다. 예를 들어 특정 개체 ID가 잠금 에스컬레이션 및 기타 목적을 위해 페이지 잠금을 소유할 수 없습니다. 그러나 페이지 잠금의 개체 ID를 잠금 값 블록에 포함할 수는 있습니다.|  
|**rsc_dbid**|**smallint**|리소스와 연관된 데이터베이스 ID입니다.|  
|**rsc_indid**|**smallint**|필요한 경우 사용할 수 있는 리소스와 연관된 인덱스 ID입니다.|  
|**rsc_objid**|**int**|리소스와 연관된 개체 ID입니다. 해당되는 경우에 한합니다.|  
|**rsc_type**|**tinyint**|리소스 유형:<br /><br /> 1 = NULL 리소스(사용되지 않음)<br /><br /> 2 = 데이터베이스<br /><br /> 3 = 파일<br /><br /> 4 = 인덱스<br /><br /> 5 = 테이블<br /><br /> 6 = 페이지<br /><br /> 7 = 키<br /><br /> 8 = 익스텐트<br /><br /> 9 = RID (행 ID)<br /><br /> 10 = 응용 프로그램|  
|**rsc_flag**|**tinyint**|내부 리소스 플래그입니다.|  
|**req_mode**|**tinyint**|잠금 요청 모드입니다. 이 열은 요청자의 잠금 모드이며 허가된 모드, 변환 모드 또는 대기 모드를 표시합니다.<br /><br /> 0 = NULL - 리소스에 허가된 액세스가 없습니다. 자리 표시자 역할을 합니다.<br /><br /> 1 = Sch-S(스키마 안전성) - 특정 세션이 스키마 요소에 대해 스키마 안전성 잠금을 보유하고 있는 동안 테이블 또는 인덱스 등의 스키마 요소가 삭제되지 않도록 합니다.<br /><br /> 2 = Sch-M(스키마 수정) - 지정한 리소스의 스키마를 변경하려는 세션이 보유해야 하는 잠금 모드입니다. 다른 세션이 표시된 개체를 참조하지 않도록 합니다.<br /><br /> 3 = S(공유) - 보유 중인 세션이 리소스에 공유된 액세스를 할 수 있도록 권한을 부여합니다.<br /><br /> 4 = U(업데이트) - 업데이트될 리소스에 대해 업데이트 잠금을 획득하도록 합니다. 나중에 업데이트할 경우를 대비해 여러 세션에서 리소스를 잠근 경우 일반적인 교착 상태 발생을 방지하기 위해 사용됩니다.<br /><br /> 5 = X(배타) - 보유 중인 세션이 리소스에 배타적으로 액세스할 수 있도록 권한을 부여합니다.<br /><br /> 6 = IS(내재된 공유) - 잠금 계층 구조의 일부 하위 리소스에 S 잠금을 설정하려는 의도를 표시합니다.<br /><br /> 7 = IU(의도 업데이트) - 잠금 계층 구조의 일부 하위 리소스에 U 잠금을 설정하려는 의도를 표시합니다.<br /><br /> 8 = IX(의도 배타) - 잠금 계층 구조의 일부 하위 리소스에 X 잠금을 설정하려는 의도를 표시합니다.<br /><br /> 9 = SIU(공유 의도 업데이트) - 잠금 계층 구조의 하위 리소스에 대한 업데이트 잠금을 획득하기 위해 리소스에 대한 공유된 액세스를 표시합니다.<br /><br /> 10 = SIX(공유 의도 배타) - 잠금 계층 구조의 하위 리소스에 대한 배타적 잠금을 획득하기 위해 리소스에 대한 공유된 액세스를 표시합니다.<br /><br /> 11 = UIX(업데이트 의도 배타) - 잠금 계층 구조의 하위 리소스에 대한 배타적 잠금을 획득하기 위해 리소스에 업데이트 잠금을 보유함을 표시합니다.<br /><br /> 12 = BU. 대량 작업에 사용합니다.<br /><br /> 13 = RangeS_S(공유 키 범위 및 공유 리소스 잠금) - 직렬화 가능 범위 검색을 표시합니다.<br /><br /> 14 = RangeS_U(공유 키 범위 및 업데이트 리소스 잠금) - 직렬화 가능 업데이트 검색을 표시합니다.<br /><br /> 15 = RangeI_N(삽입 키 범위 및 Null 리소스 잠금) - 새 키를 인덱스에 삽입하기 전에 범위를 테스트하는 데 사용됩니다.<br /><br /> 16 = RangeI_S. RangeI_N 잠금과 S 잠금의 겹쳐진 부분에 의해 생성된 키 범위 변환 잠금입니다.<br /><br /> 17 = RangeI_U. RangeI_N 잠금과 U 잠금의 겹쳐진 부분에 의해 생성된 키 범위 변환 잠금입니다.<br /><br /> 18 = RangeI_X. RangeI_N 잠금과 X 잠금의 겹쳐진 부분에 의해 생성된 키 범위 변환 잠금입니다.<br /><br /> 19 = RangeX_S. RangeI_N 잠금과 RangeS_S 잠금의 겹쳐진 부분에 의해 생성된 키 범위 변환 잠금입니다.<br /><br /> 20 = RangeX_U. RangeI_N 잠금과 RangeS_U 잠금의 겹쳐진 부분에 의해 생성된 키 범위 변환 잠금입니다.<br /><br /> 21 = RangeX_X(배타적 키 범위 및 배타적 리소스 잠금) - 범위 내에서 키를 업데이트할 때 사용되는 변환 잠금입니다.|  
|**req_status**|**tinyint**|잠금 요청의 상태입니다.<br /><br /> 1 = 허가됨<br /><br /> 2 = 변환 중<br /><br /> 3 = 대기 중|  
|**req_refcnt**|**smallint**|잠금 참조 수입니다. 트랜잭션이 특정 리소스에 대한 잠금을 확인할 때마다 참조 수가 증가합니다. 참조 수가 0이 될 때까지 잠금을 해제할 수 없습니다.|  
|**req_cryrefcnt**|**smallint**|나중에 사용하기 위해 예약되어 있습니다. 항상 0으로 설정합니다.|  
|**req_lifetime**|**int**|잠금 사용 기간 비트맵입니다. 특정 쿼리 처리 전략을 수행하는 동안 쿼리 프로세서가 쿼리의 특정 단계를 완료할 때까지 리소스에 대한 잠금을 유지 관리해야 합니다. 잠금 사용 기간 비트맵은 쿼리 프로세서 및 트랜잭션 관리자가 쿼리의 특정 단계가 완료되었을 때 해제할 수 있는 잠금 그룹을 표시하는 데 사용됩니다. 비트맵의 특정 비트는 참조 수가 0인 경우에도 트랜잭션이 끝날 때까지 보유되는 잠금을 표시하는 데 사용됩니다.|  
|**req_spid**|**int**|내부 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 잠금을 요청 하는 세션의 프로세스 ID입니다.|  
|**req_ecid**|**int**|실행 컨텍스트 ID(ECID)입니다. 병렬 작업에서 특정 잠금을 소유하고 있는 스레드를 표시하는 데 사용합니다.|  
|**req_ownertype**|**smallint**|다음은 잠금과 연관된 개체의 유형입니다.<br /><br /> 1 = 트랜잭션<br /><br /> 2 = 커서<br /><br /> 3 = 세션<br /><br /> 4 = ExSession<br /><br /> 3과 4는 각각 세션 잠금의 특별한 버전인 데이터베이스 추적 및 파일 그룹 잠금을 나타냅니다.|  
|**req_transactionID**|**bigint**|고유 트랜잭션 ID 레지스트리에 **syslockinfo** 및 프로파일러 이벤트|  
|**req_transactionUOW**|**uniqueidentifier**|DTC 트랜잭션의 UOW(작업 단위) ID를 식별합니다. MS DTC 트랜잭션이 아닌 경우에는 UOW가 0으로 설정됩니다.|  
  
## <a name="permissions"></a>사용 권한  
 을 실행하려면 서버에 대해 VIEW SERVER STATE 권한이 필요합니다.  
  
## <a name="see-also"></a>관련 항목  
 [시스템 테이블을 시스템 뷰로 매핑 &#40;TRANSACT-SQL&#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)   
 [호환성 뷰&#40;Transact-SQL&#41;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  
