---
title: 연결 속성을 지정 하 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- connection properties [ADO]
- connections [ADO]
ms.assetid: 49456201-b085-4851-9686-e814136b07be
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c198eb4c8118328d68b40deed4ab0e57ff561f9c
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/11/2018
ms.locfileid: "35272664"
---
# <a name="specifying-connection-properties"></a>연결 속성 지정
대부분의 의해 지정 된 정보를 제공할 수 있습니다는 [연결 문자열](../../../ado/guide/data/creating-a-connection-string.md) 의 속성을 설정 하 여는 **연결** 연결을 열기 전에 개체입니다. 연결 문자열에 설명 된 대로 같은 기능을 얻을 수는 예를 들어 [연결 문자열 만들기](../../../ado/guide/data/creating-a-connection-string.md) 다음 코드를 사용 하 여 합니다.  
  
```  
With objConn  
.Provider = "SQLOLEDB"  
.Properties("Data Source") = "MySqlServer"  
   .Properties("Integrated Security") = "SSPI"  
.Open  
.DefaultDatabase = "Northwind"  
End With  
```  
  
 DefaultDatabase 연결을 연 후에 설정 됩니다.  
  
> [!NOTE]
>  ADO에서 사용 하면 안 세미콜론을 포함 하는 암호 (";")의 암호는 작은따옴표로 묶여 있지 않은 한 합니다.
