# Appendix

## Cities List

City |
---  |
Pathum Thani |
Phuket |
Ayutthaya |
Chiang Mai |
Bangkok |
Samut Sakhon |
Samut Prakan |
Phetchaburi |
Kanchanaburi |
Pattaya |
Hua Hin |
Samut Songkhram |
Chonburi |

## Country Code

Country | Country Code
--------- | ----
Afghanistan | AF
Åland Islands | AX
Albania | AL
Algeria | DZ
American Samoa | AS
Andorra | AD
Angola | AO
Anguilla | AI
Antarctica | AQ
Antigua and Barbuda | AG
Argentina | AR
Armenia | AM
Aruba | AW
Australia | AU
Austria | AT
Azerbaijan | AZ
Bahamas | BS
Bahrain | BH
Bangladesh | BD
Barbados | BB
Belarus | BY
Belgium | BE
Belize | BZ
Benin | BJ
Bermuda | BM
Bhutan | BT
Bolivia | BO
Bosnia and Herzegovina | BA
Botswana | BW
Bouvet Island | BV
Brazil | BR
British Indian Ocean Territory | IO
Brunei Darussalam | BN
Bulgaria | BG
Burkina Faso | BF
Burundi | BI
Cambodia | KH
Cameroon | CM
Canada | CA
Cape Verde | CV
Cayman Islands | KY
Central African Republic | CF
Chad | TD
Chile | CL
China | CN
Christmas Island | CX
Cocos (Keeling) Islands | CC
Colombia | CO
Comoros | KM
Congo | CG
Congo, Democratic Republic | CD
Cook Islands | CK
Costa Rica | CR
Cote D"Ivoire | CI
Croatia | HR
Cuba | CU
Cyprus | CY
Czech Republic | CZ
Denmark | DK
Djibouti | DJ
Dominica | DM
Dominican Republic | DO
Ecuador | EC
Egypt | EG
El Salvador | SV
Equatorial Guinea | GQ
Eritrea | ER
Estonia | EE
Ethiopia | ET
Falkland Islands (Malvinas) | FK
Faroe Islands | FO
Fiji | FJ
Finland | FI
France | FR
French Guiana | GF
French Polynesia | PF
French Southern Territories | TF
Gabon | GA
Gambia | GM
Georgia | GE
Germany | DE
Ghana | GH
Gibraltar | GI
Greece | GR
Greenland | GL
Grenada | GD
Guadeloupe | GP
Guam | GU
Guatemala | GT
Guernsey | GG
Guinea | GN
Guinea-Bissau | GW
Guyana | GY
Haiti | HT
Heard Island and Mcdonald Islands | HM
Holy See (Vatican City State) | VA
Honduras | HN
Hong Kong | HK
Hungary | HU
Iceland | IS
India | IN
Indonesia | ID
Iran | IR
Iraq | IQ
Ireland | IE
Isle of Man | IM
Israel | IL
Italy | IT
Jamaica | JM
Japan | JP
Jersey | JE
Jordan | JO
Kazakhstan | KZ
Kenya | KE
Kiribati | KI
Korea (North) | KP
Korea (South) | KR
Kosovo | XK
Kuwait | KW
Kyrgyzstan | KG
Laos | LA
Latvia | LV
Lebanon | LB
Lesotho | LS
Liberia | LR
Libyan Arab Jamahiriya | LY
Liechtenstein | LI
Lithuania | LT
Luxembourg | LU
Macao | MO
Macedonia | MK
Madagascar | MG
Malawi | MW
Malaysia | MY
Maldives | MV
Mali | ML
Malta | MT
Marshall Islands | MH
Martinique | MQ
Mauritania | MR
Mauritius | MU
Mayotte | YT
Mexico | MX
Micronesia | FM
Moldova | MD
Monaco | MC
Mongolia | MN
Montserrat | MS
Morocco | MA
Mozambique | MZ
Myanmar | MM
Namibia | NA
Nauru | NR
Nepal | NP
Netherlands | NL
Netherlands Antilles | AN
New Caledonia | NC
New Zealand | NZ
Nicaragua | NI
Niger | NE
Nigeria | NG
Niue | NU
Norfolk Island | NF
Northern Mariana Islands | MP
Norway | NO
Oman | OM
Pakistan | PK
Palau | PW
Palestinian Territory, Occupied | PS
Panama | PA
Papua New Guinea | PG
Paraguay | PY
Peru | PE
Philippines | PH
Pitcairn | PN
Poland | PL
Portugal | PT
Puerto Rico | PR
Qatar | QA
Reunion | RE
Romania | RO
Russian Federation | RU
Rwanda | RW
Saint Helena | SH
Saint Kitts and Nevis | KN
Saint Lucia | LC
Saint Pierre and Miquelon | PM
Saint Vincent and the Grenadines | VC
Samoa | WS
San Marino | SM
Sao Tome and Principe | ST
Saudi Arabia | SA
Senegal | SN
Serbia | RS
Montenegro | ME
Seychelles | SC
Sierra Leone | SL
Singapore | SG
Slovakia | SK
Slovenia | SI
Solomon Islands | SB
Somalia | SO
South Africa | ZA
South Georgia and the South Sandwich Islands | GS
Spain | ES
Sri Lanka | LK
Sudan | SD
Suriname | SR
Svalbard and Jan Mayen | SJ
Swaziland | SZ
Sweden | SE
Switzerland | CH
Syrian Arab Republic | SY
Taiwan, Province of China | TW
Tajikistan | TJ
Tanzania | TZ
Thailand | TH
Timor-Leste | TL
Togo | TG
Tokelau | TK
Tonga | TO
Trinidad and Tobago | TT
Tunisia | TN
Turkey | TR
Turkmenistan | TM
Turks and Caicos Islands | TC
Tuvalu | TV
Uganda | UG
Ukraine | UA
United Arab Emirates | AE
United Kingdom | GB
United States | US
United States Minor Outlying Islands | UM
Uruguay | UY
Uzbekistan | UZ
Vanuatu | VU
Venezuela | VE
Viet Nam | VN
Virgin Islands, British | VG
Virgin Islands, U.S. | VI
Wallis and Futuna | WF
Western Sahara | EH
Yemen | YE
Zambia | ZM
Zimbabwe | ZW

## Product Tags

Tags mostly use for `souvenir` product to identify some properties of the product. Some tags is use for display only but some has to do with [book product API](#book). And here it is the list of tag that you should be considered about.

Tag | Meaning | Use case
--- | ------- | ---
match_passport_name | Customer information when booked must match with customer's passport detail. Also the name title for customer (which by default you don't need customer name title to book our product) | For DTAC SIM product (which is `souvenir` type). Customer detail must match to passport detail. And when to book the product, customer name title must be provide with the first name of the customer. (Ex. Mr.John)
not_require_pickup_location | Product doesn't need pickup (or delivery) location. So the `meeting_point` field when [book souvenir product]() can be omit | DTAC SIM can be pickup at the airport. So it doesn't required pickup (or delivery) location

## Meeting Points
If the trip has free hotel pickup option (as you can see `Hotel Pickup` type in `meeting_points` field from [trip detail](#get-product-detail)).
You can choose hotel pickup as a meeting point by pass the hotel name in `meeting_point` field while you're making a transaction. See [Book Product](#book-product).
<pre class="center-column">
  "meeting_points": [
    {
      "_id": "565808f321389c2c1baa5db5",
      "city": "Bangkok",
      "name": "Hotel Pickup in Bangkok Area",
      "type": "Hotel Pickup",
      "icon_name": "hotel",
      "location": {
        "lat": null,
        "lon": null
      }
    },
  ],
</pre>

For meeting point with type **Airport Rail Link Station, BTS Station and MRT Station** can have meeting point name **"Any Station"**. And here is the list of every station.

Type | Stations
--------- | ----
Airport Rail Link Station | <ul><li>Ban Thap Chang Station</li><li>Hua Mak Station</li><li>Lat Krabang Station</li><li>Makkasan Station</li><li>Phaya Thai</li><li>Ramkhamhaeng Station</li><li>Ratchaprarop Station</li><li>Suvarnabhumi Station</li></ul>
BTS Station | <ul><li>Ari</li><li>Asok</li><li>Bang Chak</li><li>Bang Na</li><li>Bang Wa</li><li>Bearing</li><li>Chit Lom</li><li>Chong Nonsi</li><li>Ekkamai</li><li>Krung Thon Buri</li><li>Mo Chit</li><li>Nana</li><li>National Stadium</li><li>On Nut</li><li>Phaya Thai</li><li>Phloen Chit</li><li>Pho Nimit</li><li>Phra Khanong</li><li>Phrom Phong</li><li>Punnawithi</li><li>Ratchadamri</li><li>Ratchathewi</li><li>Sala Daeng</li><li>Sanam Pao</li><li>Saphan Khwai</li><li>Saphan Taksin</li><li>Siam</li><li>Surasak</li><li>Talat Phlu</li><li>Thong Lo</li><li>Udom Suk</li><li>Victory Monument</li><li>Wongwian Yai</li><li>Wutthakat</li><li>Samrong</li></ul>
MRT Station | <ul><li>Bang Sue</li><li>Chatuchak Park</li><li>Hua Lamphong</li><li>Huai Khwang</li><li>Kamphaeng Phet</li><li>Khlong Toei</li><li>Lat Phrao</li><li>Lumphini</li><li>Phahon Yothin</li><li>Phetchaburi</li><li>Phra Ram 9</li><li>Queen Sirikit National Convention Centre</li><li>Ratchadaphisek</li><li>Sam Yan</li><li>Si Lom</li><li>Sukhumvit</li><li>Sutthisan</li><li>Thailand Cultural Centre</li><li>Yaek Tiwanon</li><li>Phra Nang Klao Bridge</li><li>Sam Yaek Bang Yai</li><li>Ministry of Public Health</li><li>Tao Poon</li><li>Sai Ma</li><li>Talad Bang Yai</li><li>Nonthaburi Civic Center</li><li>Bang Son</li><li>Wong Sawang</li><li>Bang Rak Noi Tha It</li><li>Khlong Bang Phai</li><li>Yaek Nonthaburi 1</li><li>Bang Krasor</li><li>Bang Phlu</li><li>Bang Rak Yai</li></ul>
