---
title: 도메인 만들기 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
f1_keywords:
- sql12.dqs.kb.createdomain.f1
ms.assetid: 5c4828f5-bd51-4c29-b3de-87b7d2f2d3e5
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 6db2481777a79697e109400786399a5db9daf448
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/11/2019
ms.locfileid: "56024454"
---
# <a name="create-a-domain"></a>도메인 만들기
  이 항목에서는 DQS( [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] )에서 도메인을 만드는 방법에 대해 설명합니다. 도메인의 값은 필드의 데이터를 의미 체계에 따라 표현한 것입니다. 도메인에 대한 자세한 내용은 [도메인 관리](../../2014/data-quality-services/managing-a-domain.md)를 참조하세요.  
  
 새 도메인을 만드는 방법에는 두 가지가 있습니다. 첫 번째는 새 기술 자료 또는 기존 기술 자료에 정보를 추가할 데이터 샘플을 분석하는 기술 자료 검색 작업의 매핑 단계에서 만드는 방법입니다. 두 번째는 도메인 관리 작업에서 기존 도메인을 변경하는 대신 새 도메인을 만드는 방법입니다.  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="Prerequisites"></a> 필수 구성 요소  
 도메인을 만들려면 기술 자료를 만들고 열어 두어야 합니다.  
  
###  <a name="Security"></a> 보안  
  
####  <a name="Permissions"></a> Permissions  
 도메인을 만들려면 DQS_MAIN 데이터베이스에 대한 dqs_kb_editor 또는 dqs_administrator 역할이 있어야 합니다.  
  
##  <a name="Discovery"></a> 기술 자료 검색 작업에서 도메인 만들기  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)] [Data Quality Client 응용 프로그램을 실행합니다](../../2014/data-quality-services/run-the-data-quality-client-application.md).  
  
2.  [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 홈 화면에서 **기술 자료 열기** 를 클릭한 다음 기술 자료를 선택하거나 **새 기술 자료** 를 클릭하고 새 기술 자료의 속성을 입력합니다.  
  
3.  **기술 자료 검색** 을 작업으로 선택한 다음 **만들기** 를 클릭하여 새 기술 자료를 만들거나 **열기** 를 클릭하여 기존 기술 자료를 엽니다.  
  
4.  **맵** 페이지에서 데이터 원본에 대한 연결을 지정합니다. 자세한 내용은 [Perform Knowledge Discovery](../../2014/data-quality-services/perform-knowledge-discovery.md)을 참조하세요.  
  
5.  **매핑** 테이블에서 빈 행의 **원본 열** 에 대한 드롭다운 목록에서 원본 열을 선택합니다. 해당 도메인이 없으면 **도메인 만들기** 아이콘을 클릭합니다.  
  
##  <a name="DomainManagement"></a> 도메인 관리 작업에서 도메인 만들기  
  
1.  [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 홈 화면에서 **기술 자료 열기** 를 클릭한 다음 기술 자료를 선택하거나 **새 기술 자료** 를 클릭하고 새 기술 자료의 속성을 입력합니다.  
  
2.  **도메인 관리** 를 작업으로 선택한 다음 **만들기** 를 클릭하여 새 기술 자료를 만들거나 **열기** 를 클릭하여 기존 기술 자료를 엽니다.  
  
3.  **도메인 관리** 페이지에서 도메인 목록 위에 있는 **도메인 만들기** 아이콘을 클릭합니다.  
  
##  <a name="Properties"></a> 도메인 속성 설정  
  
1.  **도메인 만들기** 대화 상자에서 기술 자료에 고유한 이름과 설명(최대 256자)을 입력합니다.  
  
    > [!NOTE]  
    >  도메인 속성에 대한 자세한 내용은 [Set Domain Properties](../../2014/data-quality-services/set-domain-properties.md)을 참조하십시오.  
  
2.  **데이터 형식** 목록에서 도메인 값의 데이터 형식을 선택합니다. 데이터 형식은 **문자열** (기본값), **날짜**, **정수**또는 **10진수**가 될 수 있습니다.  
  
3.  동의어 값 대신 동의어 그룹의 선행 값이 출력되도록 지정하려면 **선행 값 사용** 을 선택합니다. 각 동의어 값이 올바른 형식 또는 수정된 형식으로 출력되고 동의어 그룹의 선행 값으로 바뀌지 않도록 지정하려면 **선행 값 사용** 을 선택 취소합니다.  
  
4.  데이터 형식이 **문자열**인 경우 **문자열 정규화** 를 선택하여 도메인 값의 특수 문자를 제거하면 일치 확률을 높일 수 있습니다.  
  
5.  **출력 형식** 드롭다운 목록에서 도메인의 데이터 값이 출력될 때 적용할 서식을 선택합니다. 서식은 다음 목록에 표시된 것처럼 2단계에서 선택한 데이터 형식에 따라 달라집니다.  
  
    -   문자열 값의 경우 문자열이 대문자, 소문자로 출력되거나 앞 글자만 대문자로 출력되도록 지정할 수 있습니다.  
  
    -   날짜 값의 경우 년, 월, 일 형식으로 지정할 수 있습니다.  
  
    -   정수 값의 경우 적용할 서식 마스크의 유형을 지정할 수 있습니다.  
  
    -   10진수 값의 경우 적용할 서식 마스크의 유형과 정확도를 지정할 수 있습니다.  
  
     **출력 형식** 드롭다운 목록에서 **없음** 을 선택하면 목록의 아무런 서식도 적용되지 않습니다.  
  
6.  데이터 형식이 **문자열**인 경우 **언어** 드롭다운 목록에서 맞춤법 검사기를 설정할 경우 적용할 맞춤법 검사기의 언어 버전을 선택합니다.  
  
7.  데이터 형식이 **문자열**인 경우 도메인을 채울 때 모든 문자열 값에 대해 맞춤법 검사기를 실행하려면 **맞춤법 검사기 사용** 을 선택합니다.  
  
8.  데이터 형식이 **문자열**인 경우 문자열 값의 구문 오류를 검사하지 않고 도메인을 채우려면 **구문 오류 알고리즘 사용 안 함** 을 선택합니다.  
  
9. **확인**을 클릭합니다.  
  
10. **마침** 을 클릭하여 [도메인 관리 작업 종료](../../2014/data-quality-services/end-the-domain-management-activity.md)에 설명된 대로 도메인 관리 작업을 완료합니다.  
  
##  <a name="FollowUp"></a> 후속 작업: 도메인을 만든 후  
 도메인을 만든 후 도메인에 대해 다른 도메인 관리 태스크를 수행하거나, 기술 자료 검색을 수행하여 도메인에 정보를 추가하거나, 도메인에 일치 정책을 추가할 수 있습니다. 자세한 내용은 [기술 자료 검색 수행](../../2014/data-quality-services/perform-knowledge-discovery.md), [도메인 관리](../../2014/data-quality-services/managing-a-domain.md) 또는 [일치 정책 만들기](../../2014/data-quality-services/create-a-matching-policy.md)를 참조하세요.  
  
  
