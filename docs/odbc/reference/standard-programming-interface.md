---
title: 표준 프로그래밍 인터페이스 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC [ODBC], database access
- SQL [ODBC], database access
- database access [ODBC]
- standardizing database access [ODBC], programming interface
- programming interface standardization [ODBC]
ms.assetid: a2fa727e-51f2-4123-ae25-0ee28e611231
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c7767f113d0f70569ce253f0200cd35cb83915a4
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81279999"
---
# <a name="standard-programming-interface"></a>표준 프로그래밍 인터페이스
프로그래밍 인터페이스는 아마도 표준화를 위한 가장 확실한 후보일 것입니다. 실제로 ODBC가 개발될 때 ANSI와 ISO는 이미 임베디드 SQL 및 SQL 모듈에 대한 표준을 제공했습니다. 데이터베이스 CLI에 대한 표준은 존재하지 않지만 데이터베이스 공급업체의 산업 컨소시엄인 SQL Access Group은 데이터베이스 CLI를 만들지 여부를 고려하고 있었습니다. ODBC의 일부는 나중에 자신의 작품의 기초가되었다.  
  
 ODBC에 대한 요구 사항 중 하나는 단일 응용 프로그램 바이너리가 여러 DBMS에서 작동해야 한다는 것이었습니다. 이러한 이유로 ODBC는 포함된 SQL 또는 모듈 언어를 사용하지 않습니다. 포함된 SQL 및 모듈 언어의 언어는 표준화되어 있지만 각 언어는 DBMS 별 사전 컴파일러에 연결됩니다. 따라서 각 DBMS에 대해 응용 프로그램을 다시 컴파일해야 하며 결과 바이너리는 단일 DBMS에서만 작동합니다. 미니컴퓨터및메인프레임세계에서발견되는저용량응용은허용되지만,개인용컴퓨터세계에서는받아들일수없습니다. 첫째, 고객에게 대량의 수축 포장 소프트웨어의 여러 버전을 제공하는 것은 물류 악몽입니다. 둘째, 개인용 컴퓨터 응용 프로그램은 여러 DBMS에 동시에 액세스해야 하는 경우가 많습니다.  
  
 반면에 호출 수준 인터페이스는 각 로컬 컴퓨터에 있는 라이브러리 또는 데이터베이스 드라이버를 통해 구현할 수 있습니다. 각 DBMS에 대해 다른 드라이버가 필요합니다. 최신 운영 체제는 런타임에 이러한 라이브러리(예: Microsoft® Windows® 운영 체제)를 로드할 수 있으므로 단일 응용 프로그램은 다시 컴파일하지 않고 다른 DBMS의 데이터에 액세스할 수 있으며 동시에 여러 데이터베이스의 데이터에 액세스할 수도 있습니다. 새 데이터베이스 드라이버를 사용할 수 있게 되면 사용자는 데이터베이스 응용 프로그램을 수정, 다시 컴파일 또는 다시 연결하지 않고도 컴퓨터에 설치할 수 있습니다. 또한, 호출 수준 인터페이스는 ODBC가 원래 개발된 플랫폼인 Windows가 이미 이러한 라이브러리를 광범위하게 사용했기 때문에 ODBC에 적합한 후보였습니다.
