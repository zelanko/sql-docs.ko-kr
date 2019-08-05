---
title: 아티클 문제 | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.newpubwizard.articleissues.f1
ms.assetid: bde57da2-dd47-412f-9df7-9224968b2448
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2014||=sqlallproducts-allversions
ms.openlocfilehash: 69d0337fe66af61e66290117d94043cc01547524
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2019
ms.locfileid: "68770706"
---
# <a name="article-issues"></a>아티클 문제
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  **아티클 문제** 페이지는 아티클에 대해 검색된 조건 및 이러한 조건의 결과로 필요한 변경 내용을 나열합니다. 다음 표에서는 발생 가능한 문제 및 복제와 기존 애플리케이션이 올바르게 작동하는지 여부를 확인하는 데 필요한 동작을 나열합니다.  
  
|아티클 문제|세부 정보|필요한 동작|  
|-------------------|-------------|---------------------|  
|Uniqueidentifier 열이 테이블에 추가됩니다.|복제에는 병합 게시의 모든 아티클에 대해 데이터 형식이 **uniqueidentifier** 인 열 또는 구독 업데이트를 허용하는 트랜잭션 게시가 필요합니다.|복제에서는 첫 번째 스냅샷이 생성될 때 데이터 형식이 **uniqueidentifier** 인 열을 이 열이 없는 게시된 테이블에 자동으로 추가합니다. 이러한 테이블을 참조하는 INSERT 및 UPDATE 문이 열 목록을 사용하는지 확인해야 합니다. 또한 추가할 열에 필요한 디스크 공간이 충분한지 확인해야 합니다.|  
|IDENTITY 열에는 NOT FOR REPLICATION 옵션이 필요합니다.|복제에서 모든 IDENTITY 열은 NOT FOR REPLICATION 옵션을 사용해야 합니다. 게시된 IDENTITY 열에서 이 옵션을 사용하지 않으면 INSERT 명령이 제대로 복제되지 않습니다.|[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] 이전 버전을 실행하는 게시자에서 생성된 게시에 적용됩니다. 모든 IDENTITY 열에 대해 NOT FOR REPLICATION 속성을 지정해야 합니다.|  
|IDENTITY 속성이 구독자로 전송되지 않았습니다.|이 게시는 구독자에서의 업데이트를 허용하지 않습니다. IDENTITY 열을 구독자로 전송할 때 IDENTITY 속성은 전송되지 않습니다. 예를 들어 게시자에서 INT IDENTITY로 정의된 열은 구독자에서 INT로 정의됩니다.|[!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] 이전 버전을 실행하는 게시자에서 생성된 게시에 적용됩니다. 별도의 동작이 필요하지 않습니다.|  
|뷰에서 참조하는 테이블이 필요합니다.|[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 뷰에서 참조한 테이블 및 게시된 인덱싱된 뷰를 모두 구독자에서 사용할 수 있어야 합니다. 참조된 테이블이 이 게시에 아티클로 게시되지 않으면 구독자에서 이를 수동으로 만들어야 합니다.|**뒤로** 단추를 사용하여 **아티클** 페이지로 이동합니다. 필요한 개체를 추가합니다.|  
|저장 프로시저가 참조하는 개체가 필요합니다.|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 테이블 및 사용자 정의 함수와 같이 게시된 저장 프로시저가 참조하는 모든 개체는 구독자에서 사용할 수 있어야 합니다. 참조된 개체가 이 게시에서 아티클로 게시되지 않으면 구독자에서 이를 수동으로 만들어야 합니다.|**뒤로** 단추를 사용하여 **아티클** 페이지로 이동합니다. 필요한 개체를 추가합니다.|  
  
## <a name="see-also"></a>참고 항목  
 [데이터 및 데이터베이스 개체 게시](../../relational-databases/replication/publish/publish-data-and-database-objects.md)   
 [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)  
  
  
