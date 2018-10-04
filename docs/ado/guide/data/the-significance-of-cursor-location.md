---
title: 커서 위치의 중요성 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6d25153a3c84340ad6feea43aa969ef52d358fe4
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47717721"
---
# <a name="the-significance-of-cursor-location"></a>커서 위치의 중요성
모든 커서는 해당 데이터를 저장할 임시 리소스를 사용 합니다. 이러한 리소스는 메모리, 디스크 페이징 파일, 임시 디스크 파일 또는 데이터베이스의 임시 저장소 수 있습니다. 커서 라고 한 *클라이언트 쪽* 클라이언트 컴퓨터에서 이러한 리소스가 있는 경우에 커서입니다. 커서 라고 한 *서버측* 커서 서버에 이러한 리소스가 있는 경우.  
  
## <a name="client-side-cursors"></a>클라이언트 쪽 커서  
 Ado에서 호출 하 여 클라이언트 쪽 커서를 사용 하 여 **adUseClient CursorLocationEnum 합니다.** 서버 키 집합이 아닌 클라이언트 쪽 커서를 사용 하 여 클라이언트 컴퓨터에 네트워크에서 설정 전체 결과 보냅니다. 클라이언트 컴퓨터를 제공 하 고 커서 및 결과 집합에 필요한 임시 리소스를 관리 합니다. 클라이언트 쪽 응용 프로그램 전체 결과 집합 결정 해야 하는 행을 찾을 수 있습니다.  
  
 정적 키 집합 커서와 클라이언트 쪽 커서 너무 많은 행을 포함 하는 경우 워크스테이션에 상당한 부하를 배치할 수 있습니다. 모든 커서 라이브러리는 수천 개의 행을 사용 하 여 커서를 작성할 수 있는, 이러한 대량의 행 집합 인출 하도록 하는 응용 프로그램 성능이 떨어질 수 있습니다. 물론 예외도 있습니다. 일부 응용 프로그램에 대 한 많은 클라이언트 쪽 커서를 완벽 하 게 적합할 및 성능 문제가 되지 않을 수 있습니다.  
  
 클라이언트 쪽 커서 빠르다는 장점이 빠른 응답입니다. 결과 집합을 클라이언트 컴퓨터로 다운로드 후 행을 검색 속도가 매우 빠릅니다. 응용 프로그램은 별도 각 클라이언트 및 서버에 없는 커서의 리소스 요구 사항이 있으므로 일반적으로 클라이언트 쪽 커서를 사용 하 여 확장성.  
  
## <a name="server-side-cursors"></a>서버 쪽 커서  
 Ado에서 호출 하 여 서버 쪽 커서를 사용 하 여 **가 adUseServer CursorLocationEnum 합니다.** 서버 쪽 커서를 사용 하 여 서버 결과 서버 컴퓨터에서 제공 하는 리소스를 사용 하 여 집합을 관리 합니다. 서버 쪽 커서 네트워크를 통해 요청된 된 데이터만 반환합니다. 이 유형의 커서 과도 한 네트워크 트래픽을 문제 상황에서 특히 클라이언트 쪽 커서 보다 더 나은 성능을 제공할 경우에 따라 수 있습니다.  
  
 그러나 반드시 서버 쪽 커서는 지적-일시적으로 라도-모든 활성 클라이언트에 대 한 귀중 한 서버 리소스를 사용 합니다. 서버 하드웨어에 모든 활성 클라이언트에서 요청한 서버 쪽 커서를 관리할 수 있도록 적절 하 게 계획 해야 합니다. 또한 서버 쪽 커서를 느려질 수만 단일 행 액세스를 제공 하기 때문에-사용 가능한 batch 커서가 없습니다.  
  
 서버 쪽 커서는 삽입, 업데이트 또는 레코드를 삭제 하는 경우에 유용 합니다. 서버 쪽 커서를 사용 하 여 동일한 연결에서 다중 활성 문이 있습니다.
