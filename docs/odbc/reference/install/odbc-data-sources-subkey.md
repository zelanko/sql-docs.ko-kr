---
title: ODBC 데이터 소스 하위 키 | 마이크로 소프트 문서
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
ms.openlocfilehash: c5e97e643a78187b15e91833c832cd16ca435c7f
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304063"
---
# <a name="odbc-data-sources-subkey"></a>ODBC 데이터 소스 하위 키

하위 키 `ODBC Data Sources` 아래의 값은 데이터 원본을 나열합니다. 이러한 값의 형식은 다음 표에 나와 있습니다.

| 속성 | 데이터 형식 | 데이터 |
| :--- | :-------- | :--- |
| *데이터 원본 이름* | REG_SZ | *드라이버 설명* |
| &nbsp; | &nbsp; | &nbsp; |

*데이터 원본 이름* 값은 관리 프로그램(일반적으로 사용자에게 메시지를 표시함)에 의해 정의되며 드라이버 *설명은* 드라이버 개발자가 정의합니다(일반적으로 드라이버와 연결된 DBMS의 이름).

예를 들어 SQL Server를 사용하는 인벤토리와 같은 세 가지 데이터 원본이 정의되었다고 가정합니다. dBASE를 사용하는 급여; 및 형식이 지정된 텍스트 파일을 사용하는 담당자입니다. 하위 키 `ODBC Data Sources` 아래의 값은 다음과 같습니다.

```console
Inventory : REG_SZ : SQL Server
Payroll : REG_SZ : dBASE
Personnel : REG_SZ : Text
```
