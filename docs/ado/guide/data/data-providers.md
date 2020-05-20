---
title: 데이터 공급자 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- data providers [ADO]
- OLE DB providers [ADO]
- ADO, OLE DB providers
ms.assetid: 877b9f25-60c4-4ab6-8052-2c28a3849e89
author: rothja
ms.author: jroth
ms.openlocfilehash: 6dfb672b57b95224cf6ff056c3298c7c8a437d2a
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82761109"
---
# <a name="data-providers"></a>데이터 공급자
데이터 공급자는 SQL 데이터베이스, 인덱싱된 순차 파일, 스프레드시트, 문서 저장소, 메일 파일 등 다양 한 데이터 원본을 나타냅니다. 공급자는 행 집합 이라는 일반적인 추상화를 사용 하 여 데이터를 균일 하 게 노출 합니다.  
  
 ADO는 지정 된 공급자의 특정 기능에 관계 없이 여러 다른 데이터 공급자에 연결 하 고 동일한 프로그래밍 모델을 계속 표시할 수 있으므로 강력 하 고 유연 합니다. 그러나 각 데이터 공급자는 고유 하기 때문에 응용 프로그램이 ADO와 상호 작용 하는 방식은 데이터 공급자에 따라 달라 집니다.  
  
 예를 들어 Microsoft SQL Server 데이터베이스에 액세스 하는 데 사용 되는 SQL Server에 대 한 OLE DB 공급자의 기능과 기능은 웹 서버의 파일 저장소에 액세스 하는 데 사용 되는 Microsoft OLE DB Provider for Internet Publishing의 기능과 크게 다릅니다.
