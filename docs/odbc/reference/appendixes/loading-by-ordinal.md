---
title: 서 수로 로딩 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: fdc7728fe06df708efd973423f5c8c05333ce189
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68041604"
---
# <a name="loading-by-ordinal"></a>서수별 로드
Odbc에서 *2.x*, 서 수로 로드 연결 프로세스의 성능을 향상 시키기 위해 수행할 수 있습니다. ODBC *2.x* 드라이버 내보내기 서 수 199 사용 하 여 더미 함수; 드라이버 관리자를 감지할 때 이름이 아닌 서 수에서 ODBC 함수의 주소를 확인 합니다. ODBC에 대 한이 기능은 여전히 지원 됩니다 *2.x* 드라이버 있지만 ODBC에 대 한 지원 되지 않습니다 *3.x* 드라이버입니다.
