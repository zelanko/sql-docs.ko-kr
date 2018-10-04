---
title: sp_fulltext_service (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_fulltext_service
- sp_fulltext_service_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- full-text search [SQL Server], properties
- sp_fulltext_service
- Full-Text Search Upgrade Option
ms.assetid: 17a91433-f9b6-4a40-88c4-8c704ec2de9f
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 046c09f21f3be3b3b87a6563af6ee614c1fbd40c
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47723381"
---
# <a name="spfulltextservice-transact-sql"></a>sp_fulltext_service(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 전체 텍스트 검색의 서버 속성을 변경합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_fulltext_service [ [@action=] 'action'   
     [ , [ @value= ] value ] ]  
```  
  
## <a name="arguments"></a>인수  
 [  **@action=**] **'***동작***'**  
 변경하거나 다시 설정할 속성입니다. *동작* 됩니다 **nvarchar(100),** 기본값은 없습니다. 목록은*c*속성, 해당 설명 및 설정할 수 있는 값이 아래 표를 참조 합니다 *값* 인수입니다. 이 인수는 데이터 형식, 현재 실행 값, 최소값 또는 최대값, 사용 중단 상태(해당되는 경우)와 같은 속성을 반환합니다.  
  
 [ **@value=**] *value*  
 지정한 속성의 값입니다. *값* 됩니다 **sql_variant**, 기본값은 NULL입니다. 하는 경우 @value 이 null 이면 **sp_fulltext_service** 현재 설정을 반환 합니다. 이 표에서는 동작 속성, 설명 및 설정할 수 있는 값 목록을 보여 줍니다.  
  
> [!NOTE]  
>  다음 작업의 이후 릴리스에서 제거 됩니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **clean_up**, **connect_timeout**하십시오 **data_timeout**, 및 **resource_ 사용 현황**합니다. 향후 개발 작업에서는 이러한 동작을 사용하지 않도록 하고 현재 이러한 동작을 사용하는 응용 프로그램은 수정하십시오.  
  
|작업|데이터 형식|Description|  
|------------|---------------|-----------------|  
|**clean_up**|**int**|이전 버전과의 호환성을 위해서만 지원됩니다. 값은 항상 0입니다.|  
|**connect_timeout**|**int**|이전 버전과의 호환성을 위해서만 지원됩니다. 값은 항상 0입니다.|  
|**data_timeout**|**int**|이전 버전과의 호환성을 위해서만 지원됩니다. 값은 항상 0입니다.|  
|**load_os_resources**|**int**|운영 체제 단어 분리기, 형태소 분석기 및 필터가 이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 등록되어 사용되는지 여부를 나타냅니다. 다음 중 하나입니다.<br /><br /> 0 = 이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스와 연관된 필터와 단어 분리기만 사용합니다.<br /><br /> 1 = 운영 체제 필터와 단어 분리기를 로드합니다.<br /><br /> 기본적으로 이 속성은 운영 체제 업데이트 시 실수로 동작이 변경되는 것을 방지하기 위해 해제되어 있습니다. 운영 체제 리소스를 사용하도록 설정하면 설치된 인스턴스별 리소스가 없는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 인덱싱 서비스에 등록된 언어 및 문서 유형에 대한 리소스에 액세스할 수 있습니다. 운영 체제 리소스 로드를 사용 하도록 설정 하면 해당 운영 체제 리소스가 트러스트 된 서명 된 이진 파일; 되는지 확인 그렇지 않으면 이러한 경우 로드할 수 없습니다 **verify_signature** (아래 참조)가 1로 설정 합니다.|  
|**master_merge_dop**|**int**|마스터 병합 프로세스에서 사용할 스레드 수를 지정합니다. 이 값은 사용 가능한 CPU 또는 CPU 코어 수를 초과하면 안 됩니다.<br /><br /> 이 인수가 지정되지 않은 경우 서비스에서는 4나 사용 가능한 CPU 또는 CPU 코어 수 중에서 더 작은 수를 사용합니다.|  
|**pause_indexing**|**int**|전체 텍스트 인덱싱이 현재 실행 중인 경우 이를 일시 중지하거나, 현재 일시 중지되었다면 다시 시작할지 여부를 지정합니다.<br /><br /> 0 = 서버 인스턴스에 대한 전체 텍스트 인덱싱 작업을 다시 시작합니다.<br /><br /> 1 = 서버 인스턴스에 대한 전체 텍스트 인덱싱 작업을 일시 중지합니다.|  
|**resource_usage**|**int**|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상 버전에서는 사용할 수 없으며 무시됩니다.|  
|**update_languages**|NULL|전체 텍스트 검색에 등록된 언어 목록과 필터를 업데이트합니다. 언어는 인덱싱을 구성할 때 전체 텍스트 쿼리에 지정됩니다. 필터는 필터 데몬 호스트에서와 같은 데이터 형식으로 저장 된.docx 등 해당 파일 형식에서 텍스트 정보를 추출 하는 데 사용 됩니다 **varbinary**하십시오 **varbinary (max)**, **이미지** , 또는 **xml**, 전체 텍스트 인덱싱에 대 한 합니다.<br /><br /> 자세한 내용은 [등록된 필터와 단어 분리기 보기 및 변경](../../relational-databases/search/view-or-change-registered-filters-and-word-breakers.md)을 참조하세요.|  
|**upgrade_option**|**int**|데이터베이스를 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]에서 이상 버전으로 업그레이드할 때 전체 텍스트 인덱스를 마이그레이션하는 방법을 제어합니다. 이 속성은 데이터베이스 복사 마법사를 사용하여 데이터베이스를 연결하거나, 데이터베이스 백업 및 파일 백업을 복원하거나, 데이터베이스를 복사하여 업그레이드에 적용됩니다.<br /><br /> 다음 중 하나입니다.<br /><br /> 0 = 향상된 새 단어 분리기를 사용하여 전체 텍스트 카탈로그를 다시 작성합니다. 인덱스를 다시 작성하면 시간이 오래 걸릴 수 있으며 업그레이드 후 CPU 및 메모리가 많이 필요할 수 있습니다.<br /><br /> 1 = 전체 텍스트 카탈로그를 다시 설정합니다. [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 전체 텍스트 카탈로그 파일이 제거되지만 전체 텍스트 카탈로그 및 전체 텍스트 인덱스의 메타데이터는 유지됩니다. 업그레이드가 끝나면 모든 전체 텍스트 인덱스의 변경 내용 추적이 해제되고 탐색이 자동으로 시작되지 않습니다. 업그레이드가 완료된 후 전체 채우기를 수동으로 실행할 때까지 카탈로그가 비어 있습니다.<br /><br /> 2 = 전체 텍스트 카탈로그를 가져옵니다. 일반적으로 가져오기가 다시 작성보다 훨씬 빠릅니다. 예를 들어 CPU를 하나만 사용하는 경우 가져오기가 다시 작성보다 10배 정도 빠릅니다. 그러나 가져온 전체 텍스트 카탈로그에는 향상된 단어 분리기가 사용되지 않으므로 결국에는 전체 텍스트 카탈로그를 다시 작성해야 할 수 있습니다.<br /><br /> 참고: 다시 작성은 다중 스레드 모드로 실행할 수 있습니다 및 모든 Cpu를 사용 하도록 다시 작성을 허용 하는 경우 다시 작성 될 수 있습니다 가져오기 보다 더 빠르게 실행을 경우 둘 이상의 10 개의 Cpu가 사용할 수 있습니다.<br /><br /> 전체 텍스트 카탈로그를 사용할 수 없는 경우 연결된 전체 텍스트 인덱스가 다시 작성됩니다. 이 옵션은 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 데이터베이스에 대해서만 사용할 수 있습니다.<br /><br /> 전체 텍스트 업그레이드 옵션을 선택하는 방법은[전체 텍스트 검색 업그레이드](../../relational-databases/search/upgrade-full-text-search.md)를 참조하세요.<br /><br /> 참고:이 속성을 설정 하려면 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]를 사용 합니다 **전체 텍스트 업그레이드 옵션** 속성입니다. 자세한 내용은 [서버 인스턴스의 전체 텍스트 검색 관리 및 모니터링](../../relational-databases/search/manage-and-monitor-full-text-search-for-a-server-instance.md)을 참조하세요.|  
|**verify_signature**|**int**|전체 텍스트 엔진이 서명된 이진 파일만 로드할지 여부를 나타냅니다. 기본적으로 트러스트된 서명된 이진 파일만 로드됩니다.<br /><br /> 1 = 트러스트된 서명된 이진 파일만 로드하는지 확인합니다(기본값).<br /><br /> 0 = 이진 파일의 서명 여부를 확인하지 않습니다.|  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="result-sets"></a>결과 집합  
 없음  
  
## <a name="permissions"></a>사용 권한  
 멤버는 **serveradmin** 고정된 서버 역할 또는 시스템 관리자가 실행할 수 있습니다 **sp_fulltext_service**합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-updating-the-list-of-registered-languages"></a>1. 등록된 언어 목록 업데이트  
 다음 예에서는 전체 텍스트 검색에 등록된 언어 목록을 업데이트합니다.  
  
```  
EXEC sp_fulltext_service 'update_languages';  
GO  
```  
  
### <a name="b-changing-the-full-text-upgrade-option-to-reset-full-text-catalogs"></a>2. 전체 텍스트 카탈로그를 초기화하도록 전체 텍스트 업그레이드 옵션 변경  
 다음 예에서는 전체 텍스트 카탈로그를 초기화하도록 전체 텍스트 업그레이드 옵션을 변경합니다. 이렇게 하면 전체 텍스트 카탈로그가 완전히 제거됩니다. 이 예에서는 선택적 `@action` 및 `@value` 키워드를 지정합니다.  
  
```  
EXEC sp_fulltext_service @action='upgrade_option', @value=1;  
GO  
```  
  
## <a name="see-also"></a>관련 항목  
 [전체 텍스트 검색](../../relational-databases/search/full-text-search.md)   
 [FULLTEXTSERVICEPROPERTY&#40;Transact-SQL&#41;](../../t-sql/functions/fulltextserviceproperty-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
