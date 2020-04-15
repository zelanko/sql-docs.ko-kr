---
title: 서수로 적재 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- backward compatibility [ODBC], loading by ordinal
- compatibility [ODBC], loading by ordinal
- loading by ordinal [ODBC]
ms.assetid: 337d90ab-68eb-4940-a2f3-f7d5693ee766
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 64bff8dcdd3802f75dc402c9ada60f82580aca5c
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81288723"
---
# <a name="loading-by-ordinal"></a>서수별 로드
ODBC *2.x에서는*연결 프로세스의 성능을 향상시키기 위해 서수에 의한 로딩을 수행할 수 있습니다. ODBC *2.x* 드라이버는 서수 199와 더미 함수를 내보전; 드라이버 관리자가 이를 감지하면 ODBC 함수의 주소를 이름이 아닌 서수로 확인합니다. 이 기능은 ODBC *2.x* 드라이버에서 계속 지원되지만 ODBC *3.x* 드라이버에는 지원되지 않습니다.
