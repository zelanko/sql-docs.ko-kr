---
title: 서 수로 로드 | Microsoft Docs
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68041604"
---
# <a name="loading-by-ordinal"></a>서수별 로드
ODBC 2.x에서 서 *수를 기준*으로 로드를 수행 하 여 연결 프로세스의 성능을 향상 시킬 수 있습니다. ODBC 2.x *드라이버는* 서 수가 199 인 더미 함수를 내보냅니다. 드라이버 관리자는이를 검색할 때 이름이 아니라 서 수로 ODBC 함수의 주소를 확인 합니다. 이 기능은 ODBC 2.x 드라이버에 대해서도 지원 되지만 ODBC *3.x 드라이버에* 는 지원 되지 *않습니다.*
