---
title: 데이터 원본에 연결
description: ADO.NET의 데이터 원본에 연결하는 데 사용되는 연결 개체에 대해 알아봅니다. 선택하는 Connection 개체는 데이터 원본 유형에 따라 다릅니다.
ms.date: 11/13/2020
ms.assetid: 9abc3f92-1be3-4e1a-b360-762dc689650e
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-chmalh
ms.openlocfilehash: 26554deb5d8a3786efd1bd869a2692d368132531
ms.sourcegitcommit: debaff72dbfae91b303f0acd42dd6d99e03135a2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/01/2020
ms.locfileid: "96419814"
---
# <a name="connecting-to-a-data-source-in-adonet"></a>ADO.NET에서 데이터 원본에 연결

[!INCLUDE[appliesto-netfx-netcore-netst-md](../../includes/appliesto-netfx-netcore-netst-md.md)]

[!INCLUDE[Driver_ADONET_Download](../../includes/driver_adonet_download.md)]

Microsoft SqlClient 데이터 공급자에서 **Connection** 개체를 사용하여 연결 문자열에 필요한 인증 정보를 제공하여 특정 데이터 원본에 연결합니다. 사용하는 **Connection** 개체는 데이터 원본의 형식에 따라 다릅니다.

Microsoft SqlClient Data Provider for SQL Server에는 <xref:System.Data.Common.DbConnection> 클래스에서 파생된 <xref:Microsoft.Data.SqlClient.SqlConnection> 유형이 포함되어 있습니다.

## <a name="in-this-section"></a>섹션 내용  

[연결 설정](establishing-connection.md)\
**Connection** 개체를 사용하여 데이터 원본에 대한 연결을 설정하는 방법을 설명합니다.

[연결 이벤트](connection-events.md)\
**InfoMessage** 이벤트를 사용하여 데이터 원본에서 정보 메시지를 검색하는 방법을 설명합니다.

## <a name="see-also"></a>참조

- [연결 문자열](connection-strings.md)
- [연결 풀링](connection-pooling.md)
