---
title: 저장 프로시저에서 동의어 사용 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- stored procedures [ODBC], ODBC driver for Oracle
- ODBC driver for Oracle [ODBC], stored procedures
ms.assetid: 8620b039-a086-4534-8710-cc8b1787dc80
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6d3758aeb954427f333c5a22298d6675c04acdb5
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81292763"
---
# <a name="using-synonyms-with-stored-procedures"></a>저장 프로시저와 동의어 사용
> [!IMPORTANT]  
>  이 기능은 이후 버전의 Windows에서 제거 될 예정입니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. 대신 Oracle에서 제공 하는 ODBC 드라이버를 사용 합니다.  
  
 Oracle 저장 프로시저를 호출할 때 Oracle 버전 2.0 및 2.5 용 Microsoft ODBC 드라이버는 동의어를 지원 하지 않습니다. 동의어는 테이블과 같은 다른 Oracle 데이터베이스 개체와 함께 사용할 경우 예상 대로 작동 합니다.
