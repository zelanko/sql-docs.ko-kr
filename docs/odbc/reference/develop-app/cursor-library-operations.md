---
title: 커서 라이브러리 작업 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC cursor library [ODBC], backward compatibility
- compatibility [ODBC], cursor library
- upgrading applications [ODBC], cursor library
- application upgrades [ODBC], cursor library
- backward compatibility [ODBC], cursor library
- cursor library [ODBC], backward compatibility
ms.assetid: 04d514b1-dc4d-4b84-bf35-60f4657ef1f6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 748d917ad060609d40e40a24e5669cff37188691
ms.sourcegitcommit: 56b963446965f3a4bb0fa1446f49578dbff382e0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2019
ms.locfileid: "67792659"
---
# <a name="cursor-library-operations"></a>커서 라이브러리 작업
> [!IMPORTANT]  
>  이 기능은 Windows의 이후 버전에서 제거 됩니다. 새 개발 작업에서는이 기능을 사용 하지 말고 현재이 기능을 사용 하는 응용 프로그램은 수정 합니다. 드라이버의 커서 기능을 사용 하는 것이 좋습니다.  
  
 ODBC 사용 응용 프로그램 *2.x* 드라이버는 odbc 호출 *3.x* 커서 라이브러리를 응용 프로그램이 ODBC를 사용 하는 일을 할 수 있습니다 *3.x* 되지 않는 기능 ODBC에서 지 원하는 *2.x* 드라이버입니다. 하지만 어떻게 이러한 기능을 사용 응용 프로그램 작성기에서 주의 해야 해야 합니다. ODBC 활용 *3.x* ODBC 커서 라이브러리에 해도 *2.x* 드라이버는 ODBC *3.x* 드라이버입니다.
