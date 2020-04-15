---
title: Microsoft 구성 요소 서비스 사용 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC driver for Oracle [ODBC], component services
- component services [ODBC]
ms.assetid: 06450562-d8f3-4987-b7bd-4a70223ff937
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: fb5763058fa198cbad7464434e31942ef8d6cd7d
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307584"
---
# <a name="using-microsoft-component-services"></a>Microsoft 구성 요소 서비스 사용
> [!IMPORTANT]  
>  이 기능은 이후 버전의 Windows에서 제거됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. 대신 오라클에서 제공하는 ODBC 드라이버를 사용합니다.  
  
 오라클 데이터베이스를 활성화하여 마이크로소프트 윈도우 NT/윈도우 2000 및 마이크로소프트 윈도우 95/98에서 트랜잭션 구성 요소 서비스(또는 Windows NT를 사용하는 경우 MTS)로 작업할 수 있습니다. 오라클 데이터베이스가 트랜잭션을 지원하는 구성 요소 서비스와 함께 작동하도록 하려면 시스템 관리자는 V$XATRANS$라는 뷰를 만들어야 합니다. 이 스크립트를 만들려면 Oracle에서 제공한 스크립트를 실행해야 합니다. 자세한 내용은 구성 요소 서비스 도움말 또는 Oracle 설명서를 참조하십시오.
