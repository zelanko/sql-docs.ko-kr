---
title: "시스템 기본 테이블 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-tables
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- system base tables [SQL Server]
- hobt [SQL Server]
- base tables
ms.assetid: 31f2df90-651f-4699-8067-19f59b60904f
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 80200caa85c27f1568b02c573b51ec0bd1a7b0f1
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2017
---
# <a name="system-base-tables"></a>시스템 기본 테이블
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  시스템 기본 테이블은 특정 데이터베이스에 대한 메타데이터를 실제로 저장하는 기본 테이블입니다. **마스터** 데이터베이스는 다른 데이터베이스에 찾을 수 없는 몇 가지 추가 테이블을 포함 하기 때문에 이런 점에서 특별 합니다. 이러한 테이블에는 서버 차원 범위의 지속형 메타데이터가 들어 있습니다.  
  
> [!IMPORTANT]  
>  시스템 기본 테이블은 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 내부에서만 사용되며 일반 고객용이 아닙니다. 시스템 기본 테이블은 변경될 수 있으며 호환성이 보장되지 않습니다.  
  
## <a name="system-base-table-metadata"></a>시스템 기본 테이블 메타데이터  
 피부 여자에 게 데이터베이스에 대 한 CONTROL, ALTER 또는 VIEW DEFINITION 권한이 있는 시스템 기본 테이블 메타 데이터를 볼 수는 **sys.objects** 카탈로그 뷰에 있습니다. 피부 여 자가 이름을 확인할 수 있고 시스템 기본 테이블의 Id와 같은 기본 제공 함수를 사용 하 여 개체 [OBJECT_NAME](../../t-sql/functions/object-name-transact-sql.md) 및 [OBJECT_ID](../../t-sql/functions/object-id-transact-sql.md)합니다.  
  
 시스템 기본 테이블에 바인딩하려면 사용자는 DAC(관리자 전용 연결)를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 연결해야 합니다. DAC를 사용하여 연결하지 않고 시스템 기본 테이블에서 SELECT 쿼리를 실행하려고 하면 오류가 발생합니다.  
  
> [!IMPORTANT]  
>  DAC를 사용한 시스템 기본 테이블 액세스는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 담당자용이며 고객용이 아닙니다.  
  
## <a name="system-base-tables"></a>시스템 기본 테이블  
 다음 표에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 각 시스템 기본 테이블을 나열하고 설명합니다.  
  
|기본 테이블|Description|  
|----------------|-----------------|  
|**sys.sysschobjs**|모든 데이터베이스에 있습니다. 각 행은 데이터베이스의 개체를 나타냅니다.|  
|**sys.sysbinobjs**|모든 데이터베이스에 있습니다. 데이터베이스의 각 Service Broker 엔터티에 대한 행을 포함합니다. Service Broker 엔터티에는 다음이 포함됩니다.<br /><br /> 메시지 유형<br /><br /> 서비스 계약<br /><br /> 서비스<br /><br /> 이름 및 유형에는 고정된 이진 데이터 정렬이 사용됩니다.|  
|**sys.sysclsobjs**|모든 데이터베이스에 있습니다. 다음을 비롯한 동일한 공용 속성을 공유하는 각 분류된 엔터티에 대한 행을 포함합니다.<br /><br /> 어셈블리<br /><br /> 백업 장치<br /><br /> 전체 텍스트 카탈로그<br /><br /> 파티션 함수<br /><br /> 파티션 구성표<br /><br /> 파일 그룹<br /><br /> 난독 처리 키|  
|**sys.sysnsobjs**|모든 데이터베이스에 있습니다. 각 네임스페이스 범위의 엔터티에 대한 행을 포함합니다. 이 테이블은 XML 컬렉션 엔터티를 저장하는 데 사용됩니다.|  
|**sys.syscolpars**|모든 데이터베이스에 있습니다. 테이블, 뷰 또는 테이블 반환 함수의 모든 열에 대한 행을 포함합니다. 이 테이블에는 프로시저 또는 함수의 모든 매개 변수에 대한 행도 포함됩니다.|  
|**sys.systypedsubobjs**|모든 데이터베이스에 있습니다. 유형이 지정된 각 하위 엔터티에 대한 행을 포함합니다. 파티션 함수의 매개 변수만 이 범주에 해당합니다.|  
|**sys.sysidxstats**|모든 데이터베이스에 있습니다. 테이블 및 인덱싱된 뷰의 각 인덱스 또는 통계에 대한 행을 포함합니다.<br /><br /> 참고: 힙 제외한 모든 인덱스는 인덱스와 동일한 이름을 가진 통계와 연결 합니다.|  
|**sys.sysiscols**|모든 데이터베이스에 있습니다. 각 지속형 인덱스 및 통계 열에 대한 행을 포함합니다.|  
|**sys.sysscalartypes**|모든 데이터베이스에 있습니다. 각 사용자 정의 유형 또는 시스템 유형에 대한 행을 포함합니다.|  
|**sys.sysdbreg**|에 **마스터** 데이터베이스에 해당 합니다. 등록된 각 데이터베이스에 대한 행을 포함합니다.|  
|**sys.sysxsrvs**|에 **마스터** 데이터베이스에 해당 합니다. 각 로컬 서버, 연결된 서버 또는 원격 서버에 대한 행을 포함합니다.|  
|**sys.sysrmtlgns**|이 시스템 기본 테이블에 존재는 **마스터** 데이터베이스에 해당 합니다. 각 원격 로그인 매핑에 대한 행을 포함합니다. 이는 해당 서버에서 들어오는 로그인을 실제 로컬 로그인으로 매핑하는 데 사용됩니다.|  
|**sys.syslnklgns**|에 **마스터** 데이터베이스에 해당 합니다. 각 연결된 로그인 매핑에 대한 행을 포함합니다. 연결된 로그인 매핑은 로컬 서버에서 해당 연결된 서버로 나가는 원격 프로시저 호출 및 분산 쿼리에 사용됩니다.|  
|**sys.sysxlgns**|에 **마스터** 데이터베이스에 해당 합니다. 각 서버 보안 주체에 대한 행을 포함합니다.|  
|**sys.sysdbfiles**|모든 데이터베이스에 있습니다. 경우 열 **dbid** 가 0 이면이 데이터베이스에 속하는 파일의 행을 나타냅니다. 에 **마스터** 데이터베이스에서 열 **dbid** 0 두 일 수 있습니다. 이 경우 해당 행은 마스터 파일을 나타냅니다.|  
|**sys.sysusermsg**|에 **마스터** 데이터베이스에 해당 합니다. 각 행은 사용자 정의 오류 메시지를 나타냅니다.|  
|**sys.sysprivs**|모든 데이터베이스에 있습니다. 각 데이터베이스 또는 서버 수준 사용 권한에 대한 행을 포함합니다.<br /><br /> 참고: 서버 수준 사용 권한을에 저장 되는 **마스터** 데이터베이스입니다.|  
|**sys.sysowners**|모든 데이터베이스에 있습니다. 각 행은 데이터베이스 보안 주체를 나타냅니다.|  
|**sys.sysobjkeycrypts**|모든 데이터베이스에 있습니다. 개체와 연결된 각 대칭 키, 암호화 또는 암호화 속성에 대한 행을 포함합니다.|  
|**sys.syscerts**|모든 데이터베이스에 있습니다. 데이터베이스의 각 인증서에 대한 행을 포함합니다.|  
|**sys.sysasymkeys**|모든 데이터베이스에 있습니다. 각 행은 비대칭 키를 나타냅니다.|  
|**sys.ftinds**|모든 데이터베이스에 있습니다. 데이터베이스의 각 전체 텍스트 인덱스에 대한 행을 포함합니다.|  
|**sys.sysxprops**|모든 데이터베이스에 있습니다. 각 확장 속성에 대한 행을 포함합니다.|  
|**sys.sysallocunits**|모든 데이터베이스에 있습니다. 각 저장소 할당 단위에 대한 행을 포함합니다.|  
|**sys.sysrowsets**|모든 데이터베이스에 있습니다. 인덱스 또는 힙의 각 파티션 행 집합에 대한 행을 포함합니다.|  
|**sys.sysrowsetrefs**|모든 데이터베이스에 있습니다. 각 행 집합 참조 인덱스에 대한 행을 포함합니다.|  
|**sys.syslogshippers**|에 **마스터** 데이터베이스에 해당 합니다. 각 데이터베이스 미러링 모니터 서버에 대한 행을 포함합니다.|  
|**sys.sysremsvcbinds**|모든 데이터베이스에 있습니다. 각 원격 서비스 바인딩에 대한 행을 포함합니다.|  
|**sys.sysconvgroup**|모든 데이터베이스에 있습니다. Service Broker의 각 서비스 인스턴스에 대한 행을 포함합니다.|  
|**sys.sysxmitqueue**|모든 데이터베이스에 있습니다. 각 Service Broker 전송 큐에 대한 행을 포함합니다.|  
|**sys.sysdesend**|모든 데이터베이스에 있습니다. Service Broker 대화의 각 송신 끝점에 대한 행을 포함합니다.|  
|**sys.sysdercv**|모든 데이터베이스에 있습니다. Service Broker 대화의 각 수신 끝점에 대한 행을 포함합니다.|  
|**sys.sysendpts**|에 **마스터** 데이터베이스에 해당 합니다. 서버에 생성된 각 끝점에 대한 행을 포함합니다.|  
|**sys.syswebmethods**|에 **마스터** 데이터베이스에 해당 합니다. 서버에 생성된 SOAP 기반 HTTP 끝점에 정의된 각 SOAP 메서드에 대한 행을 포함합니다.|  
|**sys.sysqnames**|모든 데이터베이스에 있습니다. 4바이트 ID 토큰에 대한 각 정규화된 이름 또는 네임스페이스에 대한 행을 포함합니다.|  
|**sys.sysxmlcomponent**|모든 데이터베이스에 있습니다. 각 행은 XML 스키마 구성 요소를 나타냅니다.|  
|**sys.sysxmlfacet**|모든 데이터베이스에 있습니다. XML 유형 정의의 각 XML 패싯(제한)에 대한 행을 포함합니다.|  
|**sys.sysxmlplacement**|모든 데이터베이스에 있습니다. XML 구성 요소의 각 XML 배치에 대한 행을 포함합니다.|  
|**sys.syssingleobjrefs**|모든 데이터베이스에 있습니다. 일반적인 각 N 대 1 참조에 대한 행을 포함합니다.|  
|**sys.sysmultiobjrefs**|모든 데이터베이스에 있습니다. 일반적인 각 N 대 N 참조에 대한 행을 포함합니다.|  
|**sys.sysobjvalues**|모든 데이터베이스에 있습니다. 엔터티의 일반적인 각 값 속성에 대한 행을 포함합니다.|  
|**sys.sysguidrefs**|모든 데이터베이스에 있습니다. GUID로 분류된 각 ID 참조에 대한 행을 포함합니다.|  
  
  
