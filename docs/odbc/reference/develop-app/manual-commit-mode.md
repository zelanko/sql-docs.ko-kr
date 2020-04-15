---
title: 수동 커밋 모드 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- rolling back transactions [ODBC]
- manual-commit mode [ODBC]
- transactions [ODBC], commit modes
- committing transactions [ODBC]
- commit modes [ODBC]
- transactions [ODBC], rolling back
ms.assetid: 9c4b3931-e48b-4960-89a2-5697537e9f51
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2a00ff373e374d0940b3e7259eeb01e26b620cae
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81287877"
---
# <a name="manual-commit-mode"></a>수동 커밋 모드
*수동 커밋 모드에서* 응용 프로그램은 **SQLEndTran을** 호출하여 트랜잭션을 명시적으로 완료하여 커밋하거나 롤백해야 합니다. 대부분의 관계형 데이터베이스에 대한 일반 트랜잭션 모드입니다.  
  
 ODBC의 트랜잭션을 명시적으로 시작할 필요는 없습니다. 대신 응용 프로그램이 데이터베이스에서 작동을 시작할 때마다 트랜잭션이 암시적으로 시작됩니다. 데이터 원본에 명시적 트랜잭션 이시적이 필요한 경우 드라이버는 응용 프로그램이 트랜잭션을 요구하는 문을 실행할 때마다 이를 제공해야 하며 현재 트랜잭션이 없습니다.
