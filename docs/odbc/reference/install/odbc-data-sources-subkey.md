---
title: ODBC 데이터 원본 하위 키 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- subkeys [ODBC], for data sources
- data sources [ODBC], subkeys
- registry entries for data sources [ODBC], subkeys
ms.assetid: 0a8ccb80-c573-4418-84e5-f04a2b0e2ac1
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e81fe6cc77d92a8fde7530c1f79381025a05856b
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32915468"
---
# <a name="odbc-data-sources-subkey"></a>ODBC 데이터 원본 하위 키
ODBC 데이터 소스 하위 키 아래의 값에는 데이터 원본을 나열 합니다. 다음 표에 나와 있는 것 처럼 이러한 값의 형식은입니다.  
  
|이름|데이터 형식|Data|  
|----------|---------------|----------|  
|*데이터 소스 이름*|REG_SZ|*드라이버 설명*|  
  
 *데이터 소스 이름* 값 (있는 일반적으로 사용자에 대 한)는 관리 프로그램에 의해 정의 되 고 *드라이버 설명* 드라이버 개발자에 의해 정의 됩니다 (의 이름을 일반적으로 DBMS 드라이버와 관련 된)입니다.  
  
 예를 들어 3 개의 데이터 원본을 정의한: SQL Server;를 사용 하 여 인벤토리 DBASE;를 사용 하 여 급여 및 인력, 사용 하 여 서식이 지정 된 텍스트 파일입니다. ODBC 데이터 소스 하위 키 아래에 값은 다음과 같을 수 있습니다.  
  
```  
Inventory : REG_SZ : SQL Server  
Payroll : REG_SZ : dBASE  
Personnel : REG_SZ : Text  
```
