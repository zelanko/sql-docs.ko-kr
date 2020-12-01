---
title: 부동 소수점 숫자
description: Microsoft SqlClient Data Provider for SQL Server에서 부동 소수점 숫자로 작업할 때 발생하는 몇 가지 문제에 대해 알아봅니다.
ms.date: 11/13/2020
ms.assetid: 73c218c6-1c44-4402-a167-4f6262629a91
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-chmalh
ms.openlocfilehash: 12c9255e0f05d338d1c5cbe88019a9f288e4e8a5
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/25/2020
ms.locfileid: "96126448"
---
# <a name="floating-point-numbers"></a>부동 소수점 숫자

[!INCLUDE[appliesto-netfx-netcore-netst-md](../../includes/appliesto-netfx-netcore-netst-md.md)]

[!INCLUDE[Driver_ADONET_Download](../../includes/driver_adonet_download.md)]

이 항목에서는 개발자가 Microsoft SqlClient Data Provider for SQL Server에서 부동 소수점 숫자로 작업할 때 자주 발생하는 몇 가지 문제에 대해 설명합니다. 이러한 문제는 컴퓨터가 부동 소수점 숫자를 저장하는 방식 때문에 발생하며 <xref:Microsoft.Data.SqlClient>와 같은 특정 공급자에 한정된 문제가 아닙니다.

일반적으로 부동 소수점 숫자에는 정확히 일치하는 이진 표현이 없기 때문에 컴퓨터는 해당 숫자의 근사값을 저장합니다. 즉, 계산 시점에 따라 동일한 숫자를 나타내는 데 서로 다른 이진수가 사용될 수 있습니다. 이것은 부동 소수점 숫자가 한 표현에서 다른 표현으로 변환될 때 숫자의 최하위 유효 자릿수가 조금씩 달라질 수 있기 때문입니다. 이러한 변환은 대개 숫자가 한 형식에서 다른 형식으로 캐스팅될 때 발생합니다. 또한 변환이 데이터베이스 내에서 발생하는지, 데이터베이스 값을 나타내는 형식 간에서 발생하는지, 형식 간에서 발생하는지에 따라 약간씩 달라집니다. 이러한 차이로 인해 논리적으로 같은 숫자의 최하위 유효 자릿수가 달라져 서로 다른 값이 될 수 있습니다. 또한, 숫자의 전체 자릿수가 예상보다 작거나 클 수 있습니다. 따라서 문자열로 서식이 지정된 숫자는 예상과 다른 값으로 표시될 수 있습니다.

이러한 문제를 최소화하려면 사용할 수 있는 숫자 형식 중에서 가장 일치하는 숫자 형식을 사용해야 합니다. 예를 들어 SQL Server로 작업하는 경우 실수 형식의 Transact-SQL 값을 float 형식의 값으로 변환하면 정확한 숫자 값이 달라질 수 있습니다. .NET Framework에서 <xref:System.Single>을 <xref:System.Double>로 변환하는 경우에도 예기치 않은 결과가 발생할 수 있습니다. 이 두 경우 모두 애플리케이션의 모든 값이 동일한 숫자 형식을 사용하도록 하는 것이 좋습니다. 또한 고정 정밀도 decimal 형식을 사용하거나 작업 전에 부동 소수점 숫자를 고정 정밀도의 decimal 형식으로 캐스팅할 수도 있습니다.

같은 값인지 비교할 때 발생하는 문제를 해결하려면 최하위 유효 자릿수의 변화를 무시할 수 있는 방식으로 애플리케이션의 코드를 작성하는 것이 좋습니다. 예를 들어 두 숫자가 같은지 확인하기 위해 비교를 사용하는 대신 한 숫자에서 다른 숫자를 뺀 다음 그 차이가 허용 가능한 반올림 오차 내에 있는 경우 두 수가 같은 것으로 처리할 수 있습니다.
