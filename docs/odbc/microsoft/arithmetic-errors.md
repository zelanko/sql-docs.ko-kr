---
title: 산술 오류 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- arithmetic errors [ODBC]
- desktop database drivers [ODBC], arithmetic errors
ms.assetid: 1c47bfac-7455-4487-b673-6b47d2a2d756
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2e0880e1746b4b65070fb28bf8d83aadec301aa4
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68138175"
---
# <a name="arithmetic-errors"></a>산술 오류
ODBC 드라이버는 각 행을 인출할 때 SELECT 문에서 WHERE 절을 평가 합니다. 행에 산술 오류가 발생 하는 값 (예: 0으로 나누기 또는 숫자 오버플로)이 포함 된 경우 드라이버는 모든 행을 반환 하지만 산술 오류가 있는 열에 대 한 오류를 반환 합니다. 그러나 삽입 하거나 업데이트할 때 ODBC 드라이버는 첫 번째 산술 오류가 발생할 때 데이터 삽입 이나 업데이트를 중지 합니다.
