# logs and commands

uploading unreal engine game windows server build to Gamelift.
```
aws gamelift upload-build \
    --operating-system WINDOWS_2012 \
    --build-root build path \
    --name user-defined name of build \
    --build-version user-defined build number \
    --region us-east-1
```

## testing our `Gamelift-StartGameSession.py` lambda function

test response:
```
Response
{
  "PlayerSession": {
    "PlayerSessionId": "psess-8ca68375-fca3-4955-a17c-c9e9d4e2c560",
    "PlayerId": "5565226e-8944-41f5-b3f6-abab85ea91f2",
    "GameSessionId": "arn:aws:gamelift:us-east-1::gamesession/fleet-55c4e751-80c3-4595-9355-65fd21196942/gsess-1b209c3a-7835-4f79-8fa9-0d4d99761fc0",
    "FleetId": "fleet-55c4e751-80c3-4595-9355-65fd21196942",
    "FleetArn": "arn:aws:gamelift:us-east-1:620339869704:fleet/fleet-55c4e751-80c3-4595-9355-65fd21196942",
    "CreationTime": "2022-11-28 23:07:54.377000+00:00",
    "Status": "RESERVED",
    "IpAddress": "3.86.200.105",
    "DnsName": "ec2-3-86-200-105.compute-1.amazonaws.com",
    "Port": 7777
  },
  "ResponseMetadata": {
    "RequestId": "50c1bc83-d427-47cb-afb9-f601982cdaa5",
    "HTTPStatusCode": 200,
    "HTTPHeaders": {
      "x-amzn-requestid": "50c1bc83-d427-47cb-afb9-f601982cdaa5",
      "content-type": "application/x-amz-json-1.1",
      "content-length": "577",
      "date": "Mon, 28 Nov 2022 23:07:53 GMT"
    },
    "RetryAttempts": 0
  }
}

Function Logs
START RequestId: 039c2f68-3130-4cff-9177-82c12c1285fe Version: $LATEST
END RequestId: 039c2f68-3130-4cff-9177-82c12c1285fe
REPORT RequestId: 039c2f68-3130-4cff-9177-82c12c1285fe	Duration: 311.73 ms	Billed Duration: 312 ms	Memory Size: 128 MB	Max Memory Used: 66 MB	Init Duration: 378.15 ms

Request ID
039c2f68-3130-4cff-9177-82c12c1285fe
```

## testing our `GameLiftUnreal-CognitoLogin.py` lambda function

test response:
```
Test Event Name
login-success

Response
{
  "status": "success",
  "tokens": {
    "AccessToken": "eyJraWQiOiJ3dWFMNmlMdnV5YzNHWjdWMFhBZFwvSlVuUlBcL2VmQnNWM3FuY3NRaUVzY1E9IiwiYWxnIjoiUlMyNTYifQ.eyJzdWIiOiI2OGJhZjBmZC0xN2VlLTQyYjQtYjBiYi01N2RmYTIzNzcwNTgiLCJpc3MiOiJodHRwczpcL1wvY29nbml0by1pZHAudXMtZWFzdC0xLmFtYXpvbmF3cy5jb21cL3VzLWVhc3QtMV82VjhqNEhVN2YiLCJjbGllbnRfaWQiOiI2dGo0ZWt1bmkxYjlzYjkxMjg0aHZrcmIxdSIsIm9yaWdpbl9qdGkiOiI5NzY3ODMyOS03NDUwLTRkZDctYmU1Ni0yNzA4NzFiODEyNjciLCJldmVudF9pZCI6ImNjZmQ5ZTkzLWEwNGQtNDBlZS1iOGQwLWY4NWUzMDQxYjJhZiIsInRva2VuX3VzZSI6ImFjY2VzcyIsInNjb3BlIjoiYXdzLmNvZ25pdG8uc2lnbmluLnVzZXIuYWRtaW4iLCJhdXRoX3RpbWUiOjE2Njk2NzgwMjMsImV4cCI6MTY2OTY4MTYyMywiaWF0IjoxNjY5Njc4MDIzLCJqdGkiOiJiYWE2ZDZkYS0zODE3LTRjZTMtODQxYi0wOWE2YjIxMTM3NTkiLCJ1c2VybmFtZSI6Im1hcnRpbiJ9.mvP8_d2_sBBCuewAWLnqQ2ZmkDYYv3scmzvQ3r055uBNwdelLePsiRZpTuKgyIWzC361RVGWsUscG45pXhJINBzoc4s92FBq-TEL5QGoT2WsbW-pQVcN_2xgMa7iLB0xPiSLqKTsXUSj6MN4twpJZDgsWN3bZ7p2mIWoE3tiCmIY5v3O1LfjBv7UKvCC3KROt-oLY3zufKSi6Ahpk65_g635kdWyUkCTQhXsfFNXNmMSq7DDCbTr-6YiY4Ygl4w5P8EeUgqUrcR8pQfTkyAGSeXkeovAnHMSklQvUQn-0v4qzLuz_0SlVgFq9MLad1DlilyjF9fv43UDW3-wERZ6IA",
    "ExpiresIn": 3600,
    "TokenType": "Bearer",
    "RefreshToken": "eyJjdHkiOiJKV1QiLCJlbmMiOiJBMjU2R0NNIiwiYWxnIjoiUlNBLU9BRVAifQ.IeTDkoRUiDqUo5EXw0juMVvYZpkZqye3Zyfl2EnzVbbu8cWMVbxUanqYBCQKnFbcWcSuk8eN2_GOcnyobMw9nvzhqmuUevGYedn95rlLtN4CGSkcIZSS1XX_1fR0FcTcdXV7Af0I8zkmjaFwFi4eOUAgxVvXxsa5C9GKYdIPt-rWwoXWxKZsVW68H5_QKpKPQyxnEb3W4WMCesqqq8eL8rZDgdH1oE1Zvyc2vDTLsiribu7yEzqJW2Ej4Bbm88yEglFXkvgjsxxmXIsfkyTyJIUKzZFY1YNkarFfkZkMrZZZH2_4ImR_b2CB_eD5NYoXNSQU78NPL9twsayUvRmdXA.gddSE9nhk1ET85nC.0fofmS-F5lODsMA6IikLTUXbg4ttXUtFuZmAEiZ2r1tfVKVrf--uopNqjjCZwTisdftEy_d1YzZHHjCjAKqrSqvgdtUZnmi4M6SpnUslhZRS1YgPcobu5WhWA7GyEuGvUzycKQif3qYfVd8XOLNQQwZiixntEzy0Bj-b6jUYB94uzk6HqtMbbNX1FYU51mc3EiEWVddaUnR2jeqd02PmuGiCqJlLivgSYZxjgUsvEr5GwJ611xOuLZGUwx-g9xJOEIZl3Oji5cJRYHX_WaMCOw4lKj8wXpfDO1nyuY0xkMrrstvRvciiw1uCEie80BD_4n43JF4QkkfVNeqyGBvNe7ZWkQa7xB_daHLfSvXy_TwBOlvFAgiS9MhK-r9KfeXhz9THBYCKJSwdEaKzpG2jbnECXGd9PetcUDRTxZuDBlOfBXU0qfpT4eRnBk0nPXehUWe-FFp86a-JKXfpN0WNRnnWLZEX4v6vQmSmw2fbaPLe6dukncr-PShN57Ncz7dfh_qXhnip4RA73e4wEONBGtvx83AVtrw9wD4AFHWtpySxhXpaM-McHvOiffjiGZllnHTI9iEJx9lsbu1RKepY9wP_yY6VKa8h33SWh4KQhlQQhHbK7kz6znO65vRiOSjRwUKyYSVMEnV0shIWkiCFaMTPSMTuzWtCm2n9yUXs5aEBjdzDWsfF70-CwtpNNFNNEQ03ZAhImndlk2rlwgScbgnjVfVjVaSytc-L3K6TR0yK1534t5zKronpB4mWOyG5mIfPCu2vlM_dOCf6lnySLNpugvVqZatRCudzPctHU-xxDwNfirlag0yKQUth0v5oPkICNGegVIvfsR9_aaY6Hg6yqMPkRopnI9Acp88jfTFV9CDPJCgPmEiriw5gApjQO_OPrqcJ2nOcrkEsYGP8zkxvLb1MNlIVaREPf9V1SGAfOvc7XCq988kAqBkqDsIfjgfnQKjmlBEQyBrqYN8D1-ulFVn-UoF7E9iZ5sUePZ34qU_5f8rOOzAV8RDdooByQqFw41onaPaB6jPU0mylFr7rSSt7XISqhqbuK0VwDvKM5zcxFIdCvEtX-Y9t_qIETeWpIuK-hrUOYJQyfZDFOx54vAJVz93mdzh7X9MTVuiOkW_FpjBx_CJfUfYFkhbbPGYQuS-2v5b3VbY7w-CK1kBInqMD_6vi_KmrQmijfPQCow83MLTZNm0WQVkHFEp72l5gZPkn6nRYPm0-nAcJyFSjMNwPPYUt5cxthfXbi_zrZ-Gc459FJ7jvtYtuTGEhOWIN.TfClCjfGH5aafZgYlsUV7g",
    "IdToken": "eyJraWQiOiI5WUNYNllZQ0NnNXlkVmpjSThzRG4xd2hiSVwvUTN1ZDVtRmhISVhDbms0ST0iLCJhbGciOiJSUzI1NiJ9.eyJzdWIiOiI2OGJhZjBmZC0xN2VlLTQyYjQtYjBiYi01N2RmYTIzNzcwNTgiLCJlbWFpbF92ZXJpZmllZCI6dHJ1ZSwiaXNzIjoiaHR0cHM6XC9cL2NvZ25pdG8taWRwLnVzLWVhc3QtMS5hbWF6b25hd3MuY29tXC91cy1lYXN0LTFfNlY4ajRIVTdmIiwiY29nbml0bzp1c2VybmFtZSI6Im1hcnRpbiIsIm9yaWdpbl9qdGkiOiI5NzY3ODMyOS03NDUwLTRkZDctYmU1Ni0yNzA4NzFiODEyNjciLCJhdWQiOiI2dGo0ZWt1bmkxYjlzYjkxMjg0aHZrcmIxdSIsImV2ZW50X2lkIjoiY2NmZDllOTMtYTA0ZC00MGVlLWI4ZDAtZjg1ZTMwNDFiMmFmIiwidG9rZW5fdXNlIjoiaWQiLCJhdXRoX3RpbWUiOjE2Njk2NzgwMjMsImV4cCI6MTY2OTY4MTYyMywiaWF0IjoxNjY5Njc4MDIzLCJqdGkiOiJiYWVjOTVmMy05Y2UxLTRmN2ItYWExNy03NzAzMjM4NzZmZTQiLCJlbWFpbCI6IktoaWVsX01hbnRpbGxhQHN0dWRlbnQudW1sLmVkdSJ9.dhAGBcb5VYSKBF55dTCOSNVsPjVDTtHIz-a_KIvmIcR161gv0wK_C7Kf_vEQfYPa368ni6DSbUnqlYeX3NlYfIrg433ilqqIGohTIo25Ep2ZOWhEX2k1u86sI5uHau5SPzFHGsF4RevYMKBUoNEKa2cBfddZUEq9Meon9eKxhjTe7WQgHIDu3Gw7uvlPLMMKWecGNX4QJ404Q03wc9HuQqa7s8G9IbctIG-RKauly3-S1HeJoKthSpAvYBHdosHhgvTCQQKbHfYhLwlDBLLw1C31tfC8pzvY62q0HmkPidqcGznQQJGjMg8mYEf-I9z55RqEysiFevaGhN0cge6CZg"
  }
}

Function Logs
START RequestId: ce4557b7-a0a0-4907-bed3-8c09f94dd2c4 Version: $LATEST
END RequestId: ce4557b7-a0a0-4907-bed3-8c09f94dd2c4
REPORT RequestId: ce4557b7-a0a0-4907-bed3-8c09f94dd2c4	Duration: 550.21 ms	Billed Duration: 551 ms	Memory Size: 128 MB	Max Memory Used: 66 MB	Init Duration: 332.47 ms

Request ID
ce4557b7-a0a0-4907-bed3-8c09f94dd2c4
```

## testing our `POST` method in API

we enter a curl command with POST attribute in the cloud shell provided by AWS. we send a request to our API url with `/login` appended. as you see below, with a correct username and password, an *idToken* and a `success` flag is given.

> ```[cloudshell-user@ip-10-0-91-26 ~]$ curl -X POST -d '{"username": "martin", "password": "martinClass2!"}' https://61vat08j1h.execute-api.us-east-1.amazonaws.com/test/login```

> ```{"status": "success", "tokens": {"AccessToken": "eyJraWQiOiJ3dWFMNmlMdnV5YzNHWjdWMFhBZFwvSlVuUlBcL2VmQnNWM3FuY3NRaUVzY1E9IiwiYWxnIjoiUlMyNTYifQ.eyJzdWIiOiI2OGJhZjBmZC0xN2VlLTQyYjQtYjBiYi01N2RmYTIzNzcwNTgiLCJpc3MiOiJodHRwczpcL1wvY29nbml0by1pZHAudXMtZWFzdC0xLmFtYXpvbmF3cy5jb21cL3VzLWVhc3QtMV82VjhqNEhVN2YiLCJjbGllbnRfaWQiOiI2dGo0ZWt1bmkxYjlzYjkxMjg0aHZrcmIxdSIsIm9yaWdpbl9qdGkiOiJhOGU4ZDcyZS02YjY4LTQ2ODItOTJhMy04MzVjNWZmYmY3OTYiLCJldmVudF9pZCI6IjNjMmRjNDhkLWVmMWYtNDQxOS04ZWUzLWU3ZjlhNWMyNjQ1YSIsInRva2VuX3VzZSI6ImFjY2VzcyIsInNjb3BlIjoiYXdzLmNvZ25pdG8uc2lnbmluLnVzZXIuYWRtaW4iLCJhdXRoX3RpbWUiOjE2Njk3ODAxMjksImV4cCI6MTY2OTc4MzcyOSwiaWF0IjoxNjY5NzgwMTI5LCJqdGkiOiI0NDY3ZDIyNy0zZWZkLTRlOTQtYTQwYS00YjE1YzYwMmM5MDkiLCJ1c2VybmFtZSI6Im1hcnRpbiJ9.osC3NlAujMDSz7Xn7FNVp9Rv1LTgtzD7Py22sfFace5CIDfMJdsuCdg6zmeiVpSDnJL09OB5M-c_c1i3SZ5geAFrDxE8xCGuz45FfaVid5fLqN_SlQMySdOu4ovoWcynulusD5oFMV8j3ZQEz_QMiiYZEeGx226xZvxvy05gWdlE91ET-vEAGV7VbO3ZI0QqvI-v4c5TTWUNHG5biOBT4bZ6HqqRmSel_W46l_irMclAnecKVNRGSaBBeJ3kl2joQ2HaVvLqqgtMCp0mwooPnxw6FSHdmhYEpSN0-WvCxaS8sQqkOLDSzVbEPQ_7ls_Tl44P8LEowOpbtZ9BP2Ebnw", "ExpiresIn": 3600, "TokenType": "Bearer", "RefreshToken": "eyJjdHkiOiJKV1QiLCJlbmMiOiJBMjU2R0NNIiwiYWxnIjoiUlNBLU9BRVAifQ.Es-jbWP-4qaFCCgI3BA0-3Wlggt8QrJesbDJ33Aad5nDAabM-2Y_hQ37jJRymJNPvVtvJxneTjulLtf7ZE6_4rNdozFfAEIMhLVy5ttkR-LWQd-gOdfnCXFysOSwEcdQEcjMqbr4Mvg8QepwHfBWWRdlD9PNnPCuU5xvcID0j6cY41FXyYkIhWIOFT-tlo4TiqhOy0FpuHVaubxPLQqmW26a_OsCTvKPmNLWpacoGaqT47Mk2pVLyWe0H37i7_KMLFv0HTZLLh-uJFoXcwPyhirVCVkK5GhO0VFOs567K-vU4iDEGKw4qbo6WkckXC9i6NlWr0Hbt9fB7zXZnSalRQ.M6TQjh4x5NUTP9DO.yZ4mgqUI5xckhJmY8pRGo176WVg8GZFoitreQ8InnskUFXVy074q5j0cfCyFmP3CEK_MTZGSL_BE4IIn6RUPSO0OTXfnbrF7t1dB6uEuLZ_BftfcAznicrw4CF_giriLH-oWrX_95POVXBj9_na-4zHvnTvmKOn7XsCdMEHziluMdGX4Ysg_XW-DWxNR1vr96wefUzqY8rdgjvomMRPE6ieFe5bw0X081c6-Fx6UMsv7fH2ZAjTLAGYfx7mnEX9gu5CZ-bnVyxdCdU_-X-l7YE0EVMzSTpusEq_lqglNOGBSeuROWDASSlzOAPc-kbmxph021QTP9mI8K96ckVQlsjAh4axCjS_OdiB7JfbFPbI1j0NpdWvuFcvP77nKX_NZkInNF8daqsT8fPQfN0DonXlPZK69elhG0AFNZ3du49AYPS8FVjqw1b9--65WVACm5zb57OiuCJm6XeprW80fqdXSSnv0KmgDTRATzcSI41pe863Y9wEYR3Amb2NyNTvvMgXfe3gn2V10SWL80IwU-0D9tU1B2PS3HRGzUavgSW1KXQjNVML4Q6YkZazqSWqpZL0ItMcTgeq1u28uYZ_6f6tiCUnDKEAzoFOk9j-Md2VbzSQGZTvGE-O34425rxMutk4mOreFrD88BdzY_wAk7W5wpsdLCYr93pQTCm95YYxPeCinWyzqPjU04uC8OTOtOdB1mYq0My7GXJ6t2oCZfVnKl-24I-Ai8QFQT5kCy5crICLtwC8bk82z1glHYUoGSWQ4USrSff60y8tcx12E9ielXuzj9EPo3JSG4cgJakpEFcrRbE2kkMNmIzLzSqjlzHVCOvtfySDJIu69b_7iKSnQCt4ZWi6ERSpqRnHARlsSqb7Dk8_5PtnRUHRDTTRMCNLMi0ndr30CYqxsLcflgKkhFHq9dW29h9Aq9845SQtaGwUIkA6PhyvGpoHGC_xVFrpBm9Ev_2oS0_KT9P6r47mD21ZVuVCY0GZnMwErM7ju2pUC4cKCGV5OC3pDDukmKSbn0GMdfx4XOZq6IKPzOaoVZ4rRu4FcTIKuqRi1m-Jz5I6TNp1JUKSN9fCTElNCz25CafPUCjHOq_Ieyei7yl29MDonz9iFG9iFHC48Yw47VLfBCpPdLdK1EYkfu_hb6doOriVQ2L5JcGjpf_a0pBkxzYdcPYGAZ4_lZK9G9qL2hAi0CTBp09vOwX_6WzpQmvO6yugBLMSHN5gzhNh35WEZw_txUUjnf1jm2cgjk3btt4G1QzvgwXYvL_-roSFIBIvL.3gWkhxY2QQaJqMlyNLBFhA", "IdToken": "eyJraWQiOiI5WUNYNllZQ0NnNXlkVmpjSThzRG4xd2hiSVwvUTN1ZDVtRmhISVhDbms0ST0iLCJhbGciOiJSUzI1NiJ9.eyJzdWIiOiI2OGJhZjBmZC0xN2VlLTQyYjQtYjBiYi01N2RmYTIzNzcwNTgiLCJlbWFpbF92ZXJpZmllZCI6dHJ1ZSwiaXNzIjoiaHR0cHM6XC9cL2NvZ25pdG8taWRwLnVzLWVhc3QtMS5hbWF6b25hd3MuY29tXC91cy1lYXN0LTFfNlY4ajRIVTdmIiwiY29nbml0bzp1c2VybmFtZSI6Im1hcnRpbiIsIm9yaWdpbl9qdGkiOiJhOGU4ZDcyZS02YjY4LTQ2ODItOTJhMy04MzVjNWZmYmY3OTYiLCJhdWQiOiI2dGo0ZWt1bmkxYjlzYjkxMjg0aHZrcmIxdSIsImV2ZW50X2lkIjoiM2MyZGM0OGQtZWYxZi00NDE5LThlZTMtZTdmOWE1YzI2NDVhIiwidG9rZW5fdXNlIjoiaWQiLCJhdXRoX3RpbWUiOjE2Njk3ODAxMjksImV4cCI6MTY2OTc4MzcyOSwiaWF0IjoxNjY5NzgwMTI5LCJqdGkiOiI4YzJhNGQwMy1jMzNlLTQzM2ItODE4ZS0xZGRlNmUwMmQzZTIiLCJlbWFpbCI6IktoaWVsX01hbnRpbGxhQHN0dWRlbnQudW1sLmVkdSJ9.DlH3yK9xQAr3C08ZSXxYlMTDXfe7XvcVr9pVgbOpqK2HXZZlYR-rNVv3g-Ogs22gyf1iq9Cuyw1Jr-MDFrcPg9TNsQheFhiq1xOdr_QSPGCHhsANeEeSNIs7B3w0md8NDPhHx0uPzx53tcP5HsfuJiLAGOuElvmwUgIXi0jGmrJ1A0rJrO33irKR6MPCV1Gq1gmEdutoBk-PmY05H93dG24Vr53wH-TbHin6eVIfbn2rQQ4XGA0iDuE86HNfAlYXh_VX775R18OsCsn2vfX7dFCX3mxWihK0Je8Z2pRvp_oE1PT_HMp_c8ay_g-6UvidgQghRb4JEEOed8PyqD-jwA"}}```

## testing our `GET` method in API

we enter a curl command with GET attribute in the cloud shell provided by AWS. we send a request to our API url with `/startsession` appended. as you can see, we include our idToken to our command. if idToken is valid and our user is authorized, the API returns a player session with `IpAddress` and `Port`.

> ```[cloudshell-user@ip-10-0-91-26 ~]$ curl -X GET -H "Authorization: Bearer eyJraWQiOiI5WUNYNllZQ0NnNXlkVmpjSThzRG4xd2hiSVwvUTN1ZDVtRmhISVhDbms0ST0iLCJhbGciOiJSUzI1NiJ9.eyJzdWIiOiI2OGJhZjBmZC0xN2VlLTQyYjQtYjBiYi01N2RmYTIzNzcwNTgiLCJlbWFpbF92ZXJpZmllZCI6dHJ1ZSwiaXNzIjoiaHR0cHM6XC9cL2NvZ25pdG8taWRwLnVzLWVhc3QtMS5hbWF6b25hd3MuY29tXC91cy1lYXN0LTFfNlY4ajRIVTdmIiwiY29nbml0bzp1c2VybmFtZSI6Im1hcnRpbiIsIm9yaWdpbl9qdGkiOiJhOGU4ZDcyZS02YjY4LTQ2ODItOTJhMy04MzVjNWZmYmY3OTYiLCJhdWQiOiI2dGo0ZWt1bmkxYjlzYjkxMjg0aHZrcmIxdSIsImV2ZW50X2lkIjoiM2MyZGM0OGQtZWYxZi00NDE5LThlZTMtZTdmOWE1YzI2NDVhIiwidG9rZW5fdXNlIjoiaWQiLCJhdXRoX3RpbWUiOjE2Njk3ODAxMjksImV4cCI6MTY2OTc4MzcyOSwiaWF0IjoxNjY5NzgwMTI5LCJqdGkiOiI4YzJhNGQwMy1jMzNlLTQzM2ItODE4ZS0xZGRlNmUwMmQzZTIiLCJlbWFpbCI6IktoaWVsX01hbnRpbGxhQHN0dWRlbnQudW1sLmVkdSJ9.DlH3yK9xQAr3C08ZSXxYlMTDXfe7XvcVr9pVgbOpqK2HXZZlYR-rNVv3g-Ogs22gyf1iq9Cuyw1Jr-MDFrcPg9TNsQheFhiq1xOdr_QSPGCHhsANeEeSNIs7B3w0md8NDPhHx0uPzx53tcP5HsfuJiLAGOuElvmwUgIXi0jGmrJ1A0rJrO33irKR6MPCV1Gq1gmEdutoBk-PmY05H93dG24Vr53wH-TbHin6eVIfbn2rQQ4XGA0iDuE86HNfAlYXh_VX775R18OsCsn2vfX7dFCX3mxWihK0Je8Z2pRvp_oE1PT_HMp_c8ay_g-6UvidgQghRb4JEEOed8PyqD-jwA" https://61vat08j1h.execute-api.us-east-1.amazonaws.com/test/startsession```

> ```{"PlayerSession": {"PlayerSessionId": "psess-155d5a90-964e-4568-93aa-e69d28c1a8d0", "PlayerId": "23050bf3-0b64-49f4-bd03-7ce16c9d17e9", "GameSessionId": "arn:aws:gamelift:us-east-1::gamesession/fleet-55c4e751-80c3-4595-9355-65fd21196942/gsess-1b209c3a-7835-4f79-8fa9-0d4d99761fc0", "FleetId": "fleet-55c4e751-80c3-4595-9355-65fd21196942", "FleetArn": "arn:aws:gamelift:us-east-1:620339869704:fleet/fleet-55c4e751-80c3-4595-9355-65fd21196942", "CreationTime": "2022-11-30 03:52:12.013000+00:00", "Status": "RESERVED", "IpAddress": "3.86.200.105", "DnsName": "ec2-3-86-200-105.compute-1.amazonaws.com", "Port": 7777}, "ResponseMetadata": {"RequestId": "18d31c47-863d-4fbd-999b-c99a45a66f0e", "HTTPStatusCode": 200, "HTTPHeaders": {"x-amzn-requestid": "18d31c47-863d-4fbd-999b-c99a45a66f0e", "content-type": "application/x-amz-json-1.1", "content-length": "577", "date": "Wed, 30 Nov 2022 03:52:11 GMT"}, "RetryAttempts": 0}}```