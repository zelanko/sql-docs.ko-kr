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
ms.openlocfilehash: ad141939a548aa008ef7109d0adaec5b3a8c6c3d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68001990"
---
# <a name="cursor-library-operations"></a>커서 라이브러리 작업
> [!IMPORTANT]  
>  이 기능은 이후 버전의 Windows에서 제거 될 예정입니다. 새 개발 작업에서는이 기능을 사용 하지 않도록 하 고 현재이 기능을 사용 하는 응용 프로그램은 수정 하십시오. 드라이버의 커서 기능을 사용 하는 것이 좋습니다.  
  
 *Odbc 2.x 드라이버를* 사용 하 여 작업 하는 응용 프로그램 *에서 odbc 3.x 커서 라이브러리* 를 호출 하는 경우 응용 프로그램 *은 odbc 2.x 드라이버에서* 지원 하지 않는 odbc *3.x 기능을* 사용할 수 있습니다. 그러나 응용 프로그램 작성자는 이러한 기능을 사용 하는 방법에 주의 해야 합니다. *Odbc 3.x 커서 라이브러리* 를 사용 하는 경우 odbc *2.x 드라이버를* *odbc 2.x 드라이버로 만들지* 않습니다.
