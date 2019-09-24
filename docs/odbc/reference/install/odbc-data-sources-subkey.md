---
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 4d6d54d1fc7c7742bf94e91d7370f356e28b5624
ms.sourcegitcommit: 816ff47eeab157c66e0f75f18897a63dc8033502
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/24/2019
ms.locfileid: "71207691"
---
# <a name="odbc-data-sources-subkey"></a>ODBC 데이터 원본 하위 키

`ODBC Data Sources` 하위 키 아래의 값은 데이터 원본을 나열 합니다. 이러한 값의 형식은 다음 표에 나와 있습니다.

| 이름 | 데이터 형식 | data |
| :--- | :-------- | :--- |
| *data-source-name* | REG_SZ | *driver-description* |
| &nbsp; | &nbsp; | &nbsp; |

*데이터 원본 이름* 값은 관리 프로그램 (일반적으로 사용자에 게 표시 됨)에 의해 정의 되 고 *드라이버 설명은* 드라이버 개발자에 의해 정의 됩니다 (일반적으로 드라이버와 연결 된 DBMS의 이름).

예를 들어 다음과 같은 세 개의 데이터 원본이 정의 되어 있다고 가정 합니다. SQL Server를 사용 하는 인벤토리 -DBASE를 사용 하는 급여 서식 있는 텍스트 파일을 사용 하는 및 담당자 `ODBC Data Sources` 하위 키 아래에 있는 값은 다음과 같을 수 있습니다.

```console
Inventory : REG_SZ : SQL Server
Payroll : REG_SZ : dBASE
Personnel : REG_SZ : Text
```
