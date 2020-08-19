---
description: ODBC 데이터 원본 하위 키
title: ODBC 데이터 원본 하위 키 | Microsoft Docs
ms.custom: ''
ms.date: 09/23/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- subkeys [ODBC], for data sources
- data sources [ODBC], subkeys
- registry entries for data sources [ODBC], subkeys
ms.assetid: 0a8ccb80-c573-4418-84e5-f04a2b0e2ac1
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9897c68d110f59d03ac8e1b3e403ed21844082fb
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88448935"
---
# <a name="odbc-data-sources-subkey"></a>ODBC 데이터 원본 하위 키

하위 키 아래의 값은 `ODBC Data Sources` 데이터 원본을 나열 합니다. 이러한 값의 형식은 다음 표에 나와 있습니다.

| Name | 데이터 형식 | 데이터 |
| :--- | :-------- | :--- |
| *데이터 원본-이름* | REG_SZ | *드라이버-설명* |
| &nbsp; | &nbsp; | &nbsp; |

*데이터 원본 이름* 값은 관리 프로그램 (일반적으로 사용자에 게 표시 됨)에 의해 정의 되 고 *드라이버 설명은* 드라이버 개발자에 의해 정의 됩니다 (일반적으로 드라이버와 연결 된 DBMS의 이름).

예를 들어, SQL Server를 사용 하는 Inventory 라는 세 개의 데이터 원본이 정의 되어 있다고 가정 합니다. -DBASE를 사용 하는 급여 서식 있는 텍스트 파일을 사용 하는 및 담당자 하위 키 아래에 있는 값은 다음과 같을 수 `ODBC Data Sources` 있습니다.

```console
Inventory : REG_SZ : SQL Server
Payroll : REG_SZ : dBASE
Personnel : REG_SZ : Text
```
