---
title: '작업 9: 참조 데이터 서비스 구성 | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: d0535fce-2bf5-4f6d-b517-ffe6fa13738d
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: e4c756463c43ede8c6dae0cda0a184f0ec7f9956
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "70154929"
---
# <a name="task-9-configuring-a-reference-data-service"></a>태스크 9: 참조 데이터 서비스 구성
  이 태스크에서는 Azure Marketplace에서 참조 데이터 서비스를 사용 하도록 DQS를 구성 합니다. 다음 태스크에서는이 서비스를 사용 하도록 **주소 유효성 검사** 도메인을 구성 합니다. 런타임에 정리 작업을 수행 하는 동안 DQS는 **주소 유효성 검사** 도메인의 도메인 값을 정리를 위해 서비스에 전달 합니다. 자세한 내용은 [참조 데이터를 사용 하도록 DQS 구성을](https://msdn.microsoft.com/library/hh213070.aspx) 참조 하세요.  
  
1.  **DQS 클라이언트**의 기본 페이지에 있는 **관리** 창에서 **구성**을 클릭 합니다.  
  
2.  **참조 데이터** 탭이 활성 상태 인지 확인 합니다.  
  
3.  프록시 서버를 사용 하 여 인터넷에 연결 해야 하는 경우 **네트워크 설정** 영역에서 **프록시 서버** 및 **포트** 필드에 적절 한 값을 입력 합니다.  
  
4.  **DataMarket 계정 ID** 필드에 대 한 **Azure Marketplace 계정 키** 를 입력 합니다.  
  
     ![Azure 데이터 마켓 참조 데이터 서비스 계정](../../2014/tutorials/media/et-configuringareferencedataservice.jpg "Azure 데이터 마켓 참조 데이터 서비스 계정")  
  
5.  텍스트 상자 옆 **의 유효성 검사** 단추를 클릭 하 여 계정 ID의 유효성을 검사 합니다.  
  
6.  메시지 상자에서 **확인** 을 클릭합니다.  
  
7.  페이지 맨 아래에 있는 **닫기** 를 클릭 하 여 DQS 클라이언트의 기본 페이지로 전환 합니다.  
  
## <a name="next-task"></a>다음 태스크  
 [태스크 10: 참조 데이터 서비스를 사용하도록 복합 도메인 구성](../../2014/tutorials/task-10-configuring-composite-domain-to-use-reference-data-service.md)  
  
  
