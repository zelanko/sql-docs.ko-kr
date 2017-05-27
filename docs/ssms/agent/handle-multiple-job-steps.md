---
title: "다중 작업 단계 처리 | Microsoft 문서"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- job steps [SQL Server Agent]
- ordering job steps [SQL Server]
- multiple job steps
- SQL Server Agent jobs, job steps
- control of flow for jobs [SQL Server]
ms.assetid: 7aba19ff-72b3-45f6-8e54-23f4988d63a8
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 6c7474d555c03a9ce9d02afaf613146e7d638ba8
ms.contentlocale: ko-kr
ms.lasthandoff: 04/11/2017

---
# <a name="handle-multiple-job-steps"></a>다중 작업 단계 처리
작업에 둘 이상의 작업 단계가 있는 경우에는 작업 단계가 실행되는 순서를 지정해야 합니다. 이를 *흐름 제어**라고 합니다.* 언제든지 새 작업 단계를 추가하고 작업 단계의 흐름을 다시 정렬할 수 있습니다. 변경 내용은 다음에 작업이 실행될 때 적용됩니다. 다음 그림에서는 데이터베이스 백업 작업에 대한 흐름 제어를 보여 줍니다.  
  
![SQL Server 에이전트 작업 단계 흐름 제어](../../ssms/agent/media/dbflow01.gif "SQL Server 에이전트 작업 단계 흐름 제어")  
  
첫 번째 단계는 데이터베이스 백업입니다. 이 단계가 실패하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 에이전트에서 알림을 받도록 정의된 운영자에게 실패를 보고합니다. 데이터베이스 백업 단계가 성공적으로 수행되면 다음 단계인 고객 데이터 "스크러빙"으로 진행합니다. 이 단계가 실패하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 에이전트에서 데이터베이스 복원으로 건너뜁니다. 고객 데이터 "스크러빙"이 성공적으로 수행되면 다음 단계인 통계 업데이트로 진행하는 등 마지막 단계인 성공 보고 또는 실패 보고까지 계속 진행합니다.  
  
각 작업 단계의 성공과 실패에 대한 흐름 제어 동작을 정의하려면 작업 단계가 성공할 때 취해야 할 작업과 실패할 때 취해야 할 동작을 지정해야 합니다. 또한 실패한 작업 단계의 경우에는 재시도 횟수와 재시도 간의 간격을 정의할 수 있습니다.  
  
> [!NOTE]  
> [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 에이전트 GUI(그래픽 사용자 인터페이스)를 사용하여 다중 단계 작업에서 단계를 하나 이상 삭제하면 GUI는 모든 작업 단계를 제거한 후 나머지 단계를 올바른 성공 시 또는 실패 시 참조와 함께 다시 추가합니다. 예를 들어 5개의 단계로 이루어진 작업이 있으며 첫 번째 단계가 성공적으로 완료되면 4단계로 이동하도록 구성되었다고 가정해 보십시오. 3단계를 삭제하면 GUI는 이 작업의 모든 단계를 제거하고 나머지 4개의 단계(1, 2, 4, 5)를 수정된 참조와 함께 추가합니다. 이 경우 1단계가 성공적으로 완료되면 3단계로 이동하도록 1단계의 참조가 다시 구성됩니다.  
  
작업 단계는 독립적이어야 합니다. 즉, 한 작업에서 작업 단계 간에 부울 값, 데이터 또는 숫자 값을 전달할 수 없습니다. 그러나 영구 테이블이나 전역 임시 테이블을 사용하면 한 [!INCLUDE[tsql](../../includes/tsql_md.md)] 작업 단계에서 다른 작업 단계로 값을 전달할 수 있습니다. 파일을 사용하여 실행 프로그램을 실행하는 작업 단계의 값을 한 작업 단계에서 다른 작업 단계로 전달할 수 있습니다. 예를 들어 하나의 작업 단계에서 실행되는 실행 파일이 파일에 기록하면 이후 작업 단계에서 실행되는 실행 파일은 해당 파일을 읽습니다.  
  
> [!NOTE]  
> 반복 작업 단계(작업 단계 1 다음에 작업 단계 2가 실행된 다음 작업 단계 2가 작업 단계 1로 되돌아감)를 만들 경우 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)]를 사용하여 작업을 만들면 경고 메시지가 표시됩니다.  
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 에이전트에서 작업과 작업 단계 정보를 작업 기록에 기록합니다.  
  
## <a name="see-also"></a>참고 항목  
[sp_add_job](http://msdn.microsoft.com/en-us/6ca8fe2c-7b1c-4b59-b4c7-e3b7485df274)  
[sysjobhistory](http://msdn.microsoft.com/en-us/1b1fcdbb-2af2-45e6-bf3f-e8279432ce13)  
[sysjobs(Transact-SQL)](http://msdn.microsoft.com/en-us/e244a6a5-54c2-47a6-8039-dd1852b0ae59)  
[sysjobsteps](http://msdn.microsoft.com/en-us/978b8205-535b-461c-91f3-af9b08eca467)  
[작업 구현](../../ssms/agent/implement-jobs.md)  
[작업 단계 관리](../../ssms/agent/manage-job-steps.md)  
  

