---
title: 단일 인스턴스로 정책 가져오기 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
ms.assetid: bc5bcd87-663f-41d9-bb7b-b3e083cd63df
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: 410f3a317a9d3ad2f8cab52d9f57fd4a63c1c36c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62865102"
---
# <a name="import-the-policies-to-a-single-instance"></a>단일 인스턴스로 정책 가져오기
  이 태스크에서는 단일 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]인스턴스에서 예약할 최선의 구현 방법 정책을 정책 기반 관리로 가져옵니다.  
  
## <a name="prerequisites"></a>사전 요구 사항  
 [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] 이상 버전이 실행되는 서버에서 이 절차를 수행해야 합니다.  
  
### <a name="import-the-best-practices-policies-for-the-database-engine"></a>데이터베이스 엔진에 대한 최선의 구현 방법 정책 가져오기  
  
1.  [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]를 시작하고 [!INCLUDE[ssDE](../includes/ssde-md.md)]에 연결합니다.  
  
2.  개체 탐색기에서 **관리**를 확장한 다음 **정책 관리**를 확장합니다.  
  
3.  **정책**을 마우스 오른쪽 단추로 클릭한 다음 **정책 가져오기**를 클릭합니다.  
  
4.  에 **가져올** 대화 상자에서 다음을 **가져올 파일** 상자에서 줄임표를 클릭 ( **...** ) 단추입니다.  
  
5.  **찾는 위치** 목록에서 최선의 구현 방법 정책이 포함된 다음 폴더를 찾습니다.  
  
     **C:\Program 파일 (x86) \Microsoft SQL Server\110\Tools\Policies\DatabaseEngine\1033**  
  
    > [!NOTE]  
    >  파일 경로는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 프로그램 파일의 설치 위치, 32비트 운영 체제를 실행하는지 아니면 64비트 운영 체제를 실행하는지 여부 및 언어 식별자에 따라 달라질 수 있습니다.  
  
6.  **정책 선택** 대화 상자에서 하나 이상의 정책 파일을 선택합니다.  
  
     인접하지 않은 파일을 선택하려면 파일 한 개를 클릭하고 Ctrl 키를 누른 채 추가 파일을 각각 클릭합니다. 인접 파일을 선택하려면 시퀀스의 첫 번째 파일을 클릭하고 Shift 키를 누른 채 마지막 파일을 클릭합니다.  
  
7.  파일 선택을 마쳤으면 **열기**를 클릭합니다.  
  
8.  **가져오기** 대화 상자에서 **정책 상태** 목록이 **가져올 때 정책 상태 유지** (기본값)로 설정되어 있는지 확인한 다음 **확인**을 클릭합니다.  
  
     정책을 **정책 관리** 아래의 **정책**노드로 가져옵니다. 가져온 정책은 기본적으로 "요청 시" 평가 모드로 설정됩니다.  
  
## <a name="next-steps"></a>다음 단계  
 [정책 예약](../../2014/tutorials/schedule-the-policies.md)  
  
  
