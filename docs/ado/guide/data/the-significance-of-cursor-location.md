---
description: 커서 위치의 중요성
title: 커서 위치의 의미 Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- server-side cursors [ADO]
- cursors [ADO], client-side
- client-side cursors [ADO]
- cursors [ADO], server-side
ms.assetid: 70ef5b1c-0459-41a1-b796-031f61a29a8a
author: rothja
ms.author: jroth
ms.openlocfilehash: 1ee12680e5d5acd0d4091e0c1864ae51b285a0e6
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88979354"
---
# <a name="the-significance-of-cursor-location"></a>커서 위치의 중요성
모든 커서는 임시 리소스를 사용 하 여 데이터를 저장 합니다. 이러한 리소스는 메모리, 디스크 페이징 파일, 임시 디스크 파일 또는 데이터베이스의 임시 저장소 일 수 있습니다. 이러한 리소스를 클라이언트 컴퓨터에 배치할 때 커서를 *클라이언트 쪽* 커서 라고 합니다. 이러한 리소스가 서버에 있으면 커서를 *서버측* 커서 라고 합니다.  
  
## <a name="client-side-cursors"></a>클라이언트 쪽 커서  
 ADO에서 AdUseClient CursorLocationEnum를 사용 하 여 클라이언트측 커서에 대해를 호출 **합니다.** 키가 아닌 클라이언트 쪽 커서를 사용 하면 서버는 네트워크를 통해 전체 결과 집합을 클라이언트 컴퓨터로 보냅니다. 클라이언트 컴퓨터는 커서 및 결과 집합에 필요한 임시 리소스를 제공 하 고 관리 합니다. 클라이언트 쪽 응용 프로그램은 전체 결과 집합을 검색 하 여 필요한 행을 확인할 수 있습니다.  
  
 정적 및 키 집합 기반 클라이언트 쪽 커서에 너무 많은 행이 포함 되어 있으면 워크스테이션에 상당한 부하가 생길 수 있습니다. 모든 커서 라이브러리는 수천 개의 행이 있는 커서를 작성할 수 있지만 이러한 많은 행 집합을 인출 하도록 디자인 된 응용 프로그램은 제대로 작동 하지 않을 수 있습니다. 물론 예외도 있습니다. 일부 응용 프로그램의 경우에는 많은 클라이언트 쪽 커서가 완벽 하 게 적합할 수 있으며 성능이 문제가 되지 않을 수 있습니다.  
  
 클라이언트 쪽 커서의 한 가지 분명 한 혜택은 빠른 응답입니다. 결과 집합을 클라이언트 컴퓨터로 다운로드 한 후 행을 검색 하는 것은 매우 빠릅니다. 커서의 리소스 요구 사항은 서버가 아닌 별도의 각 클라이언트에 배치 되기 때문에 일반적으로 클라이언트 쪽 커서를 사용 하 여 응용 프로그램의 확장성이 향상 됩니다.  
  
## <a name="server-side-cursors"></a>서버 쪽 커서  
 ADO에서 **AdCursorLocationEnum erver** 를 사용 하 여 서버 쪽 커서에 대해를 호출 합니다. 서버 쪽 커서를 사용 하 여 서버 컴퓨터에서 제공 하는 리소스를 사용 하 여 결과 집합을 관리 합니다. 서버측 커서는 네트워크를 통해 요청 된 데이터만 반환 합니다. 이러한 유형의 커서는 때때로 네트워크 트래픽이 과도 하 게 문제가 있는 경우에 클라이언트 쪽 커서 보다 더 나은 성능을 제공할 수 있습니다.  
  
 그러나 서버 쪽 커서가 모든 활성 클라이언트에 대해 일시적으로 사용 되는 귀중 한 서버 리소스를 가리키도록 하는 것이 중요 합니다. 서버 하드웨어가 활성 클라이언트에서 요청 하는 모든 서버 쪽 커서를 관리할 수 있도록 적절 하 게 계획 해야 합니다. 또한 서버 쪽 커서는 단일 행 액세스만 제공 하므로 사용 가능한 일괄 처리 커서가 없으므로 속도가 느릴 수 있습니다.  
  
 서버 쪽 커서는 레코드를 삽입, 업데이트 또는 삭제 하는 경우에 유용 합니다. 서버 쪽 커서를 사용 하 여 동일한 연결에서 여러 활성 문을 사용할 수 있습니다.
