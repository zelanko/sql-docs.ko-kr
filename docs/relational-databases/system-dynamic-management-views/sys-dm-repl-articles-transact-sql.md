---
title: sys. dm_repl_articles (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_repl_articles_TSQL
- dm_repl_articles
- dm_repl_articles_TSQL
- sys.dm_repl_articles
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_repl_articles dynamic management function
ms.assetid: 794d514e-bacd-432e-a8ec-3a063a97a37b
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: e102411819a28e5798779a19c6f12f57b80fdd35
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82833718"
---
# <a name="sysdm_repl_articles-transact-sql"></a>sys.dm_repl_articles(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  복제 토폴로지에 아티클로 게시된 데이터베이스 개체에 대한 정보를 반환합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**artcache_db_address**|**varbinary(8)**|게시 데이터베이스에 대한 캐시된 데이터베이스 구조의 메모리 내 주소입니다.|  
|**artcache_table_address**|**varbinary(8)**|게시된 테이블 아티클에 대한 캐시된 테이블 구조의 메모리 내 주소입니다.|  
|**artcache_schema_address**|**varbinary(8)**|게시된 테이블 아티클에 대한 캐시된 아티클 스키마 구조의 메모리 내 주소입니다.|  
|**artcache_article_address**|**varbinary(8)**|게시된 테이블 아티클에 대한 캐시된 아티클 구조의 메모리 내 주소입니다.|  
|**artid**|**bigint**|이 테이블 내의 각 항목을 고유하게 식별합니다.|  
|**artfilter**|**bigint**|아티클을 행 필터링하는 데 사용된 저장 프로시저의 ID입니다.|  
|**artobjid**|**bigint**|게시된 개체의 ID입니다.|  
|**artpubid**|**bigint**|아티클이 속한 게시의 ID입니다.|  
|**artstatus**|**tinyint**|아티클 옵션 및 상태의 비트 마스크이며 다음 값 중 하나 이상에 대한 논리적 비트 OR 연산의 결과일 수 있습니다.<br /><br /> **1** = 아티클이 활성 상태입니다.<br /><br /> **8** = INSERT 문에 열 이름을 포함 합니다.<br /><br /> **16** = 매개 변수가 있는 문을 사용 합니다.<br /><br /> **24** = INSERT 문에 열 이름을 포함 하 고 매개 변수가 있는 문을 사용 합니다.<br /><br /> 예를 들어 매개 변수가 있는 문을 사용하는 활성 아티클은 이 열의 값이 17이 되며 값 0은 아티클이 비활성 상태이고 추가 속성이 정의되지 않았음을 의미합니다.|  
|**arttype**|**tinyint**|아티클 유형입니다.<br /><br /> **1** = 로그 기반 아티클입니다.<br /><br /> **3** = 수동 필터가 있는 로그 기반 아티클입니다.<br /><br /> **5** = 수동 뷰가 있는 로그 기반 아티클입니다.<br /><br /> **7** = 수동 필터 및 수동 뷰가 있는 로그 기반 아티클입니다.<br /><br /> **8** = 저장 프로시저 실행<br /><br /> **24** = serialize 할 수 있는 저장 프로시저 실행<br /><br /> **32** = 저장 프로시저 (스키마 전용)입니다.<br /><br /> **64** = 뷰 (스키마 전용)입니다.<br /><br /> **128** = 함수 (스키마 전용)입니다.|  
|**wszArtdesttable**|**nvarchar (514)**|대상에 게시된 개체의 이름입니다.|  
|**wszArtdesttableowner**|**nvarchar (514)**|대상에 게시된 개체의 소유자입니다.|  
|**wszArtinscmd**|**nvarchar (510)**|삽입에 사용된 명령 또는 저장 프로시저입니다.|  
|**cmdTypeIns**|**int**|삽입 저장 프로시저에 대한 호출 구문이며 다음 값 중 하나가 될 수 있습니다.<br /><br /> **1** = 호출<br /><br /> **2** = SQL<br /><br /> **3** = 없음<br /><br /> **7** = 알 수 없음|  
|**wszArtdelcmd**|**nvarchar (510)**|삭제에 사용된 명령 또는 저장 프로시저입니다.|  
|**cmdTypeDel**|**int**|삭제 저장 프로시저에 대한 호출 구문이며 다음 값 중 하나가 될 수 있습니다.<br /><br /> **0** = XCALL<br /><br /> **1** = 호출<br /><br /> **2** = SQL<br /><br /> **3** = 없음<br /><br /> **7** = 알 수 없음|  
|**wszArtupdcmd**|**nvarchar (510)**|업데이트에 사용된 명령 또는 저장 프로시저입니다.|  
|**cmdTypeUpd**|**int**|업데이트 저장 프로시저에 대한 호출 구문이며 다음 값 중 하나가 될 수 있습니다.<br /><br /> **0** = XCALL<br /><br /> **1** = 호출<br /><br /> **2** = SQL<br /><br /> **3** = 없음<br /><br /> **4** = MCALL<br /><br /> **5** = VCALL<br /><br /> **6** = SCALL<br /><br /> **7** = 알 수 없음|  
|**wszArtpartialupdcmd**|**nvarchar (510)**|부분 업데이트에 사용된 명령 또는 저장 프로시저입니다.|  
|**cmdTypePartialUpd**|**int**|부분 업데이트 저장 프로시저에 대한 호출 구문이며 다음 값 중 하나가 될 수 있습니다.<br /><br /> **2** = SQL|  
|**numcol**|**int**|열 필터링된 아티클에 대한 파티션의 열 수입니다.|  
|**artcmdtype**|**tinyint**|현재 복제 중인 명령의 유형이며 다음 값 중 하나가 될 수 있습니다.<br /><br /> **1** = 삽입<br /><br /> **2** = 삭제<br /><br /> **3** = 업데이트<br /><br /> **4** = UPDATETEXT<br /><br /> **5** = 없음<br /><br /> **6** = 내부용 으로만 사용<br /><br /> **7** = 내부용 으로만 사용<br /><br /> **8** = 부분 업데이트|  
|**artgeninscmd**|**nvarchar (510)**|아티클에 포함된 열을 기반으로 하는 INSERT 명령 템플릿입니다.|  
|**artgendelcmd**|**nvarchar (510)**|사용한 호출 구문에 따라 기본 키 또는 아티클의 열을 포함할 수 있는 DELETE 명령 템플릿입니다.|  
|**artgenupdcmd**|**nvarchar (510)**|사용한 호출 구문에 따라 기본 키, 업데이트된 열 또는 전체 열 목록을 포함할 수 있는 UPDATE 명령 템플릿입니다.|  
|**artpartialupdcmd**|**nvarchar (510)**|기본 키와 업데이트된 열을 포함하는 부분 UPDATE 명령 템플릿입니다.|  
|**artupdtxtcmd**|**nvarchar (510)**|기본 키와 업데이트된 열을 포함하는 UPDATETEXT 명령 텍스트입니다.|  
|**artgenins2cmd**|**nvarchar (510)**|동시 스냅샷 처리 중 아티클을 조정하는 데 사용된 INSERT 명령 템플릿입니다.|  
|**artgendel2cmd**|**nvarchar (510)**|동시 스냅샷 처리 중 아티클을 조정하는 데 사용된 DELETE 명령 템플릿입니다.|  
|**fInReconcile**|**tinyint**|동시 스냅샷 처리 중 아티클이 현재 조정되고 있는지 여부를 나타냅니다.|  
|**fPubAllowUpdate**|**tinyint**|게시가 업데이트 구독을 허용하는지 여부를 나타냅니다.|  
|**intPublicationOptions**|**bigint**|추가 게시 옵션을 지정하는 비트맵입니다. 이때 비트 옵션 값은 다음과 같습니다.<br /><br /> **0x1** -피어 투 피어 복제에 사용 됩니다.<br /><br /> **0x2** -로컬 변경 내용만 게시 합니다.<br /><br /> **0x4** -SQL Server 이외 구독자에 사용할 수 있습니다.|  
  
## <a name="permissions"></a>사용 권한  
 **Dm_repl_articles**를 호출 하려면 게시 데이터베이스에 대 한 VIEW DATABASE STATE 권한이 필요 합니다.  
  
## <a name="remarks"></a>설명  
 현재 복제 아티클 캐시에 로드되어 있는 복제된 데이터베이스 개체에 대한 정보만 반환됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;동적 관리 뷰 및 함수](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [복제 관련 동적 관리 뷰 &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/replication-related-dynamic-management-views-transact-sql.md)  
  
  

