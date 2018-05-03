---
title: 커서 위치의 중요성 | Microsoft Docs
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- server-side cursors [ADO]
- cursors [ADO], client-side
- client-side cursors [ADO]
- cursors [ADO], server-side
ms.assetid: 70ef5b1c-0459-41a1-b796-031f61a29a8a
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3b979966c2a879ea41ff559a6b554efdbf11ca3d
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="the-significance-of-cursor-location"></a>커서 위치의 중요성
모든 커서는 해당 데이터를 저장할 임시 리소스를 사용 합니다. 이러한 리소스는 메모리, 디스크 페이징 파일, 임시 디스크 파일 또는 데이터베이스의 임시 저장소 될 수 있습니다. 커서 라고는 *클라이언트 쪽* 이러한 리소스는 클라이언트 컴퓨터에 있을 때 커서입니다. 커서 라고는 *서버 쪽* 커서 서버에 이러한 리소스가 있는 경우.  
  
## <a name="client-side-cursors"></a>클라이언트 쪽 커서  
 Ado에서 호출 하 여 클라이언트 쪽 커서를 사용 하 여 **adUseClient CursorLocationEnum 합니다.** 서버는 키 집합이 아닌 클라이언트 쪽 커서를 전체 결과 클라이언트 컴퓨터에 네트워크를 통해 집합을 보냅니다. 클라이언트 컴퓨터를 제공 하 고 커서 및 결과 집합에 필요한 임시 리소스를 관리 합니다. 클라이언트 쪽 응용 프로그램 전체 결과 집합 결정 필요한 행을 찾을 수 있습니다.  
  
 너무 많은 행을 포함 하는 경우 정적 및 키 집합 구동 클라이언트 쪽 커서 워크스테이션에 상당한 부하를 배치할 수 있습니다. 모든 커서 라이브러리는 수천 개의 행으로 커서를 작성할 수 있는, 이러한 대량의 행 집합을 인출 하는 설계 된 응용 프로그램 성능이 떨어질 수 있습니다. 예외은 물론 합니다. 일부 응용 프로그램에 대 한 큰 클라이언트 쪽 커서를 완벽 하 게 수행할 수 있습니다 및 성능 문제가 되지 않을 수 있습니다.  
  
 클라이언트 쪽 커서 빠르다는 장점이 빠른 응답입니다. 결과 집합을 클라이언트 컴퓨터로 다운로드 후 행을 검색 속도가 매우 빠릅니다. 응용 프로그램은 별도 각 클라이언트 및 서버에 없는 커서의 리소스 요구 사항이 있으므로 일반적으로 확장성이 뛰어난 클라이언트 쪽 커서를 사용 합니다.  
  
## <a name="server-side-cursors"></a>서버 쪽 커서  
 Ado에서 호출 하 여 서버 쪽 커서를 사용 하 여 **가 adUseServer CursorLocationEnum 합니다.** 서버 쪽 커서를 서버에 서버 컴퓨터에서 제공 하는 리소스를 사용 하 여 resultset을 관리 합니다. 서버 쪽 커서 네트워크를 통해 요청된 된 데이터를 반환합니다. 이러한 유형의 커서 보다 클라이언트 쪽 커서 네트워크 트래픽이 증가할 문제가 경우에 특히 더 나은 성능을 제공 수 있습니다.  
  
 서버 쪽 커서는 사실을 알아야 하는 반면-적어도 일시적으로-모든 활성 클라이언트에 대 한 귀중 한 서버 리소스를 사용 합니다. 서버 하드웨어에 모든 활성 클라이언트에서 요청한 서버 쪽 커서를 관리할 수 있도록 적절 하 게 계획 해야 합니다. 또한 서버 쪽 커서가 수만 단일 행으로의 액세스를 제공 하기 때문에 느려질 수-사용할 수 있는 일괄 처리 커서가 없습니다.  
  
 서버 쪽 커서는 삽입, 업데이트 또는 레코드를 삭제 하는 경우에 유용 합니다. 서버 쪽 커서와 동일한 연결에서 다중 활성 문을 수도 있습니다.
