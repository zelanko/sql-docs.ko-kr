---
title: "Microsoft COM 기반 해결 프로그램 | Microsoft 문서"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- COM-based resolvers [SQL Server replication]
- custom resolvers [SQL Server replication]
ms.assetid: a6637e4b-4e6b-40aa-bee6-39d98cc507c8
caps.latest.revision: 38
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: b0389bb0387489b581aae3225fd1a02e7bc9d713
ms.contentlocale: ko-kr
ms.lasthandoff: 04/11/2017

---
# <a name="advanced-merge-replication-conflict---com-based-resolvers"></a>고급 병합 복제 충돌 - COM 기반 해결 프로그램
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 와 함께 제공되는 모든 COM 기반 해결 프로그램은 업데이트 충돌을 처리하고 표시가 된 곳에서 삽입 및 삭제 충돌도 처리합니다. 모든 해결 프로그램은 열 추적을 처리하며 대부분의 경우 행 추적도 처리합니다. 이러한 해결 프로그램 및 다른 모든 COM 기반 해결 프로그램은 처리할 수 있는 충돌 유형을 선언하며 병합 에이전트는 다른 모든 충돌 유형에 대해 기본 해결 프로그램을 사용합니다.  
  
 해결 프로그램은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]설치 과정 중에 설치됩니다. **sp_enumcustomresolvers** 저장 프로시저를 실행하면 컴퓨터에 등록된 모든 충돌 해결 프로그램을 볼 수 있습니다. 프로시저를 실행하면 별개의 결과 집합에 각 해결 프로그램의 설명 및 GUID(Globally unique identifier)가 표시됩니다.  
  
 해결 프로그램을 지정하려면 [Specify a Merge Article Resolver](../../../relational-databases/replication/publish/specify-a-merge-article-resolver.md)을 참조하십시오.  
  
 다음 표에서는 특정 해결 프로그램의 특성을 설명합니다.  
  
|이름|필수 입력|설명|주석|  
|----------|--------------------|-----------------|--------------|  
|[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Additive Conflict Resolver|합계할 행 이름입니다. **int**, **smallint**, **numeric**과 같은 산술 데이터 형식이어야 합니다.|충돌 시 적용되는 내용은 우선 순위 값으로 결정합니다. 지정된 열의 값은 원본 및 대상 열 값의 합계로 설정됩니다. 하나를 NULL로 설정하면, 모두 다른 열의 값으로 설정됩니다.|업데이트 충돌 및 열 추적만 지원합니다.|  
|[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Averaging Conflict Resolver|평균할 열 이름입니다. **int**, **smallint**, **numeric**과 같은 산술 데이터 형식이어야 합니다.|충돌 시 적용되는 내용은 우선 순위 값으로 결정합니다. 결과 열 값은 원본 및 대상 열 값의 평균으로 설정됩니다. 하나를 NULL로 설정하면, 모두 다른 열의 값으로 설정됩니다.|업데이트 충돌 및 열 추적만 지원합니다.|  
|[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] DATETIME (Earlier Wins) Conflict Resolver|충돌 시 우선 적용 사항을 결정하는 데 사용한 열 이름입니다. **datetime** 데이터 형식이어야 합니다.|이전 **datetime** 값이 있는 열에 따라 충돌 시 적용되는 내용이 결정됩니다. 한 행이 NULL로 설정된 경우 다른 값이 들어 있는 행의 변경 내용이 적용됩니다.|업데이트 충돌, 행 및 열 추적을 지원합니다. 열 값은 직접 비교되고 다른 표준 시간대에 대해서는 조정이 이루어지지 않습니다.|  
|[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] DATETIME (Later Wins) Conflict Resolver|충돌 시 우선 적용 사항을 결정하는 데 사용한 열 이름입니다. **datetime** 데이터 형식이어야 합니다.|이후 **datetime** 값이 있는 열에 따라 충돌 시 적용되는 내용이 결정됩니다. 한 행이 NULL로 설정된 경우 다른 값이 들어 있는 행의 변경 내용이 적용됩니다.|업데이트 충돌, 행 및 열 추적을 지원합니다.|  
|[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Maximum Conflict Resolver|충돌 시 우선 적용 사항을 결정하는 데 사용한 열 이름입니다. **int**, **smallint**, **numeric**과 같은 산술 데이터 형식이어야 합니다.|더 큰 숫자 값을 가진 열에 따라 충돌 시 우선 적용 사항이 결정됩니다. 한 행이 NULL로 설정된 경우 다른 값이 들어 있는 행의 변경 내용이 적용됩니다.|행 및 열 추적을 지원합니다.|  
|[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Minimum Conflict Resolver|충돌 시 우선 적용 사항을 결정하는 데 사용한 열 이름입니다. **int**, **smallint**, **numeric**과 같은 산술 데이터 형식이어야 합니다.|더 작은 숫자 값을 가진 열에 따라 충돌 시 우선 적용 사항이 결정됩니다. 한 행이 NULL로 설정된 경우 다른 값이 들어 있는 행의 변경 내용이 적용됩니다.|업데이트 충돌, 행 및 열 추적을 지원합니다.|  
|[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Merge Text Conflict Resolver|`@resolver_info = '[col1][===]'`와 같은 텍스트 열 이름 및 구분 기호입니다.|충돌 시 적용되는 내용은 우선 순위 값으로 결정합니다. 충돌이 발생한 텍스트 열은 병합된 값으로 설정되며 이 값은 순서대로 공용 접두사, 게시자의 고유 부분, 구분 기호 및 구독자의 고유 부분으로 구성됩니다.|업데이트 충돌 및 열 추적만 지원합니다.|  
|[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Subscriber Always Wins Conflict Resolver|입력이 없습니다.|원본 또는 대상 위치에 관계없이 구독자의 변경 내용이 적용됩니다.|모든 충돌 유형을 지원합니다.|  
|[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Priority Column Resolver|충돌 시 우선 적용 사항을 결정하는 데 사용한 열 이름입니다. **int**, **smallint**, **numeric**과 같은 산술 데이터 형식이어야 합니다.|더 큰 숫자 값을 가진 열에 따라 충돌 시 우선 적용 사항이 결정됩니다. 한 행이 NULL로 설정된 경우 다른 값이 들어 있는 행의 변경 내용이 적용됩니다.|업데이트 충돌, 행 및 열 추적을 지원합니다.|  
|[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Upload Only Conflict Resolver|입력이 없습니다.|게시자로 업로드된 변경 내용을 받아들이며 변경 내용은 구독자로 다운로드되지 않습니다.|모든 충돌 유형을 지원합니다.|  
|[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Download Only Conflict Resolver|입력이 없습니다.|게시자로 업로드된 변경 내용은 거부되며 변경 내용은 구독자로 다운로드됩니다.|모든 충돌 유형을 지원합니다.|  
|[!INCLUDE[msCoName](../../../includes/msconame-md.md)] SQLServer 저장 프로시저 해결 프로그램|해결 프로그램에서 충돌을 해결하기 위해 호출해야 하는 저장 프로시저의 이름입니다.|충돌 해결은 사용자가 지정한 저장 프로시저의 논리에 따라 다릅니다.|업데이트 충돌을 지원합니다. 자세한 내용은 [병합 아티클용 사용자 지정 충돌 해결 프로그램 구현](../../../relational-databases/replication/implement-a-custom-conflict-resolver-for-a-merge-article.md)을 참조하세요.|  
  
## <a name="see-also"></a>참고 항목  
 [Advanced Merge Replication Conflict Detection and Resolution](../../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md)   
 [sp_enumcustomresolvers&#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-enumcustomresolvers-transact-sql.md)  
  
  
