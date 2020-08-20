---
description: '6단계: 데이터 원본 연결 끊기'
title: '6 단계: 데이터 원본에서 연결 끊기 | Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- application process [ODBC], disconnecting from data source
- data sources [ODBC], disconnecting
- disconnecting from data source [ODBC]
ms.assetid: 6ad759ba-4721-4d8f-9b26-de976d4fc1a0
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 06b3b50653578388ca3d4e20b598f63879f38e88
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88461345"
---
# <a name="step-6-disconnect-from-the-data-source"></a>6단계: 데이터 원본 연결 끊기
마지막 단계는 다음 그림과 같이 데이터 원본에서 연결을 끊는 것입니다. 첫째, 응용 프로그램은 **Sqlfreehandle**을 호출 하 여 문 핸들을 해제 합니다. 자세한 내용은 [문 핸들 해제](../../../odbc/reference/develop-app/freeing-a-statement-handle-odbc.md)를 참조 하세요.  
  
 ![데이터 소스에서 연결을 끊는 방법](../../../odbc/reference/develop-app/media/pr17.gif "pr17")  
  
 그런 다음 **Sqldisconnect** 를 사용 하 여 데이터 원본에서 응용 프로그램의 연결을 끊고 **sqlfreehandle**을 사용 하 여 연결 핸들을 해제 합니다. 자세한 내용은 [데이터 원본 또는 드라이버에서 연결 끊기](../../../odbc/reference/develop-app/disconnecting-from-a-data-source-or-driver.md)를 참조 하세요.  
  
 마지막으로 응용 프로그램은 **Sqlfreehandle** 을 사용 하 여 환경 핸들을 해제 하 고 드라이버 관리자를 언로드합니다. 자세한 내용은 [환경 핸들 할당](../../../odbc/reference/develop-app/allocating-the-environment-handle.md)을 참조 하세요.
