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
ms.openlocfilehash: 32e3fcaf9c83c2613a1dc2df499f11c7df2570ad
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63042139"
---
# <a name="cursor-library-operations"></a>커서 라이브러리 작업
> [!IMPORTANT]  
>  이 기능은 Windows의 이후 버전에서 제거 됩니다. 새 개발 작업에서는이 기능을 사용 하지 말고 현재이 기능을 사용 하는 응용 프로그램은 수정 합니다. 드라이버의 커서 기능을 사용 하는 것이 좋습니다.  
  
 ODBC 2를 사용 하 여 작업 응용 프로그램 *.x* 드라이버 호출을 ODBC 3. *x* 커서 라이브러리를 응용 프로그램이 ODBC 3을 사용 하는 일을 할 수 있습니다. *x* ODBC 2에서 지원 되지 않는 기능 *.x* 드라이버입니다. 하지만 어떻게 이러한 기능을 사용 응용 프로그램 작성기에서 주의 해야 해야 합니다. ODBC 3 사용 합니다. *x* 커서 라이브러리는 ODBC 2 해도 *.x* 드라이버는 ODBC 3. *x* 드라이버입니다.
