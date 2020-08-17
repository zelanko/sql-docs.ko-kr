---
description: 이진 형식으로 데이터 전송
title: 이진 형식으로 데이터 전송 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], transferring in binary form
- transferring data in binary form [ODBC]
- binary data transfers [ODBC]
ms.assetid: 4b12a9de-51d0-416a-87f4-9bf84959cad9
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ec858729e76c1e360ec0933eca3a29ab17542f4f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88386329"
---
# <a name="transferring-data-in-its-binary-form"></a>이진 형식으로 데이터 전송
응용 프로그램은 동일한 DBMS 및 하드웨어 플랫폼을 사용 하는 두 데이터 원본 간에 데이터 (지정 된 DBMS에서 사용 하는 내부 양식)를 안전 하 게 전송할 수 있습니다. 지정 된 데이터 조각에 대해 SQL 데이터 형식은 원본 및 대상 데이터 원본에서 동일 해야 합니다. C 데이터 형식은 SQL_C_BINARY입니다.  
  
 응용 프로그램이 **Sqlfetch**, **Sqlfetchscroll**또는 **SQLGetData** 를 호출 하 여 원본 데이터 원본에서 데이터를 검색 하는 경우 드라이버는 데이터 원본에서 데이터를 검색 하 고 변환 하지 않고 SQL_C_BINARY 형식의 저장소 위치로 전송 합니다. 응용 프로그램에서 **SQLBulkOperations**, **sqlexecute**, **sqlexecdirect**, **sqlputdata 또는 SQLSetPos** 를 호출 하 여 데이터를 대상 데이터 원본으로 보내는 경우 드라이버는 저장소 위치에서 데이터를 검색 하 고 변환 하지 않고 대상 데이터 원본으로 전송 합니다.  
  
> [!NOTE]  
>  이러한 방식으로 데이터를 전송 하는 응용 프로그램 (이진 데이터 제외)은 Dbms 간에 상호 운용할 수 없습니다.  
  
 **Sqlcopydesc** 는 원본 dbms에서 대상 dbms의 매개 변수 바인딩으로 행 바인딩을 복사 하는 데 사용할 수 있습니다.
