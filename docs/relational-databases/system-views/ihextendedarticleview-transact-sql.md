---
title: IHextendedArticleView (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- IHextendedArticleView_TSQL
- IHextendedArticleView
dev_langs:
- TSQL
helpviewer_keywords:
- IHextendedArticleView view
ms.assetid: 19ef0a12-3214-4bb0-9c25-a665897e65a2
author: stevestein
ms.author: sstein
ms.openlocfilehash: 0abca8ca826ec986a9cbf71f4fb577291e095e39
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68029537"
---
# <a name="ihextendedarticleview-transact-sql"></a>IHextendedArticleView(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  합니다 **IHextendedArticleView** 뷰는 SQL Server 이외 게시 내의 아티클에 대 한 정보를 표시 합니다. 이 보기에 저장 되는 **배포** 데이터베이스입니다.  
  
|열 이름|데이터 형식|설명|  
|-----------------|---------------|-----------------|  
|**publisher_id**|**smallint**|게시자에 대한 고유 식별자입니다.|  
|**publication_id**|**int**|게시에 대한 고유 식별자입니다.|  
|**article**|**sysname**|아티클의 이름입니다.|  
|**destination_object**|**sysname**|구독자에 게시된 개체의 이름입니다.|  
|**source_owner**|**sysname**|게시자에 게시된 개체의 소유자입니다.|  
|**source_object**|**sysname**|게시자에 게시된 개체의 이름입니다.|  
|**description**|**nvarchar(255)**|아티클 설명입니다.|  
|**creation_script**|**nvarchar(255)**|아티클에 대한 스키마 생성 스크립트입니다.|  
|**del_cmd**|**nvarchar(255)**|DELETE를 위해 실행되는 명령입니다.|  
|**filter**|**int**|수평 분할을 정의하는 데 사용되는 저장 프로시저에 대한 식별자입니다.|  
|**filter_clause**|**ntext**|아티클을 수평 분할하는 데 사용되는 WHERE 절입니다.|  
|**ins_cmd**|**nvarchar(255)**|INSERT를 위해 실행되는 명령입니다.|  
|**pre_creation_cmd**|**tinyint**|DROP TABLE, DELETE TABLE 또는 TRUNCATE에 대한 사전 생성 명령입니다.<br /><br /> **0** = none입니다.<br /><br /> **1** = DROP.<br /><br /> **2** = DELETE.<br /><br /> **3** = TRUNCATE.|  
|**상태**|**tinyint**|아티클 옵션 및 상태의 비트 마스크이며 다음 값 중 하나 이상에 대한 논리 비트 OR 연산의 결과일 수 있습니다.<br /><br /> **1** = 아티클이 활성 상태입니다.<br /><br /> **8** = INSERT 문에 열 이름을 포함 합니다.<br /><br /> **16** = 문을 매개 변수화 사용 합니다.<br /><br /> **24** = INSERT 문에 열 이름을 포함 하 고 매개 변수가 있는 문을 사용 하 여 둘 다.<br /><br /> 예를 들어 매개 변수가 있는 문을 사용 하는 활성 아티클은 값 미칠 **17** 이 열에 있습니다. 값이 **0** 는 아티클이 활성 상태입니다. 추가 속성 없이 정의 된 의미 합니다.|  
|**type**|**tinyint**|아티클 유형입니다.<br /><br /> **1** = 로그 기반 아티클입니다.<br /><br /> **3** = 수동 필터가 있는 로그 기반 아티클입니다.<br /><br /> **5** = 수동 뷰가 있는 로그 기반 아티클입니다.<br /><br /> **7** = 수동 필터 및 수동 뷰가 있는 로그 기반 아티클입니다.|  
|**upd_cmd**|**nvarchar(255)**|UPDATE를 위해 실행되는 명령입니다.|  
|**schema_option**|**binary**|스크립팅할 것을 표시 합니다. 참조 [sp_addarticle &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md) 지원 되는 스키마 옵션의 목록에 대 한 합니다.|  
|**dest_owner**|**sysname**|대상 데이터베이스에 게시된 개체의 소유자입니다.|  
  
## <a name="see-also"></a>관련 항목  
 [다른 유형의 데이터베이스 복제](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [복제 테이블 &#40;TRANSACT-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [복제 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
