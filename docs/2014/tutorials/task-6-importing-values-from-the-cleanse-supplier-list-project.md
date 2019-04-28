---
title: '태스크 6: 값 가져오기는 Cleanse Supplier List 프로젝트 | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: fec0deef-a729-4ff1-b709-72d2b3f407ac
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 0780636d3bcaecfe0519192bd450bb538d78bbf9
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62866785"
---
# <a name="task-6-importing-values-from-the-cleanse-supplier-list-project"></a>태스크 6: 값 가져오기는 Cleanse Supplier List 프로젝트
  이 작업에서는 정리 프로세스 중에 수집된 데이터 품질 기술 자료를 가져옵니다. 자세한 내용은 [정리 프로젝트 값을 도메인으로 가져오기](https://msdn.microsoft.com/library/hh479581.aspx) 항목을 참조하십시오. 또한 업데이트된 **Suppliers** 기술 자료를 게시하기 전에 기술 자료를 DQS로 내보냅니다.  
  
1.  **DQS 클라이언트**의 기본 페이지에서 **최근 기술 자료** 아래에 있는 **Suppliers** 옆에서 **오른쪽 화살표** 를 클릭하고 **도메인 관리**를 클릭합니다.  
  
2.  도메인 목록에서 **Contact Email** 을 클릭하고 오른쪽 창에서 **도메인 값** 탭으로 전환합니다.  
  
3.  도구 모음에서 **값 가져오기** 아이콘 옆의 **아래쪽 화살표** 를 클릭하고 **프로젝트 값 가져오기**를 클릭합니다.  
  
     ![프로젝트 가져오기 도구 모음 단추를 값](../../2014/tutorials/media/et-importingvaluesfromthecslistproject-01.jpg "가져오기 프로젝트 값 도구 모음 단추")  
  
4.  **프로젝트 값 가져오기** 대화 상자에서 **Cleanse Supplier List** 프로젝트를 선택하고 **확인**을 클릭합니다.  
  
5.  모든 전자 메일은 대화형 정리 중 수행한 두 가지 수정 사항을 거쳐서 가져오기가 수행됩니다. 두 가지 수정 사항을 보려면 화면을 스크롤합니다.  
  
    |값|다음으로 수정|  
    |-----------|----------------|  
    |bobby0@adventure-work.com|bobby0@adventure-works.com|  
    |tad0@adventure-work.com|tad0@adventure-works.com|  
  
6.  에 대 한 프로젝트 값 가져오기는 이전 단계를 반복 합니다 **국가** 도메인 및 수정 하기 위해 새 항목이 추가 되는 통지 **United State** 하 **미국** (사용 하 여 ' s').  
  
    |값|다음으로 수정|  
    |-----------|----------------|  
    |United State|미국|  
  
7.  이전 도메인 값을 보려면 **새 항목만 표시** 확인란의 선택을 취소합니다.  
  
8.  **Supplier Name** 도메인에 대해 이전의 프로젝트 값 가져오기 단계를 반복합니다. 기본적으로 가져오기를 수행한 후에는 새 값만 표시됩니다. 모든 값을 보려면 **새 항목만 표시** 확인란의 선택을 취소합니다. 정리 작업에서 배운 내용을 활용해서 **Suppliers** 기술 자료의 데이터가 강화되었습니다. 기술 자료가 강력할수록 정리 결과도 향상됩니다.  
  
    > [!NOTE]  
    >  복합 도메인에 대해서는 값을 가져올 수 없습니다.  
  
9. 도구 모음에서 **기술 자료 내보내기** 아이콘을 클릭한 후 **기술 자료 내보내기**를 클릭합니다.  
  
     ![기술 자료 내보내기 메뉴](../../2014/tutorials/media/et-importingvaluesfromthecslistproject-02.jpg "기술 자료 내보내기 메뉴")  
  
10. 자습서 폴더로 이동하고 **파일 이름** 으로 **Suppliers.dqs**를 입력하고 **저장**을 클릭합니다. 이 DQS 파일을 기반으로 사용해서 새로운 기술 자료를 만들 수 있습니다.  
  
11. 클릭 **확인** 닫으려면 합니다 **기술 자료 내보내기-Suppliers** 메시지 상자.  
  
12. **마침** 을 클릭하여 작업을 마칩니다.  
  
13. **게시**를 클릭합니다.  
  
14. 메시지 상자에서 **확인** 을 클릭합니다.  
  
## <a name="next-step"></a>다음 단계  
 [3단원: 공급자 목록에서 중복 제거할 데이터 일치](../../2014/tutorials/lesson-3-matching-data-to-remove-duplicates-from-supplier-list.md)  
  
  
