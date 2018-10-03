---
title: 부록-1 (OracleToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: e01f8be5-ce68-4c9f-bd13-d65e73a16470
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.openlocfilehash: c7e4b188d72e52608f8768a3d50c0d0af2af747d
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47807811"
---
# <a name="appendix---1-oracletosql"></a>부록 - 1(OracleToSQL)
SSMA 콘솔 명령줄 옵션에 대 한 빠른 보기:  
  
|Sl 합니다. 아니요.|스위치|필수 여부|스위치 인수|허용 되는 값|  
|-----------|----------|-------------|-------------------|--------------------|  
|1|-s/script|사용자 계정 컨트롤|scriptfile|올바른 XML 파일 이름입니다.<br /><br />콘솔 스크립트 정의 파일입니다.|  
|2|-v/변수|아니요|variablevaluefile|올바른 XML 파일 이름입니다.<br /><br />스크립트 파일에서 변수를 사용 하는이 파일을 지정 해야 합니다.|  
|3|-c/serverconnection|아니요|serverconnectionfile|올바른 XML 파일 이름입니다.<br /><br />이 파일 서버 연결 정보를 포함 합니다.|  
|4|-x/xmloutput|아니요|xmloutputfile|이 옵션은 XML 형식으로 콘솔 출력을 나타냅니다. 이 옵션을 지정 하지 않으면 기본 출력을 텍스트 형식으로 됩니다.<br /><br />Xmloutputfile를 지정 하지 않은 경우 XML 출력은 `STDOUT`합니다.<br /><br />Xmloutputfile에는 콘솔 출력은 XML 형식으로 기록 되는 파일의 이름입니다.|  
|5|-l/로그|아니요|logfile|유효한 파일 이름입니다.|  
|6|-e/projectenvironment|아니요|projectenvironmentfolder|SSMA 프로젝트 환경 파일이 포함 된 올바른 폴더 이름입니다.|  
|7|-p/securepassword|아니요|-추가 {< server_id > [, n] &#124; 모든}-c&#124;serverconnection < 서버 연결 파일 > [-v&#124;변수 < 변수 값 파일 >] [-o/덮어쓰기]<br /><br />로 구분하거나 여러<br /><br />-추가 {< server_id > [, n] &#124; 모든}-s&#124;스크립트 < 스크립트 파일 > [-v&#124;변수 < 변수 값 파일 >] [-o/덮어쓰기]<br /><br />– r/제거 {< server_id > [, n] &#124; 모든}<br /><br />-l/목록<br /><br />– e 내보낼 {< 서버 id > [, n] &#124; 모든} < 암호화 암호-파일 ><br /><br />– i 가져오기 / {< 서버 id > [, n] &#124; 모든} < 암호화 암호-파일 >|를 지정 하는 경우이 옵션 다른 옵션과 함께 사용할 수 없습니다.<br /><br />서버 id: {string} 서버에 대해 제공 된 고유 ID<br /><br />서버 연결 파일: 서버 정의 파일 (serverconnectionfile 또는 scriptfile).<br /><br />변수 값 파일: 변수 정의 파일을 되며 서버 연결 파일에 사용 합니다.<br /><br />암호화 암호-파일:이 파일은 서버 암호 파일 사용자 지정 암호를 사용 하 여 암호화 합니다.|  
|8|-?|아니요|해당 사항 없음|해당 사항 없음|  
  
## <a name="see-also"></a>관련 항목  
[SSMA 콘솔 (Oracle)를 실행합니다.](http://msdn.microsoft.com/en-us/7228ccba-c69f-4b4c-8664-01a2750183c5)  
  
