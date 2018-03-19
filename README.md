# bodley2
CELL's research into the earliest holdings of the Bodleian Library

## 1.0 Methodological and technical framework

### 1.1 rationale 

This project relies on a dataset which consists of bibliographical information taken from the early records of the Bodleian Library. These archival records form the original foundation of the Bodleian's early information systems, i.e. catalogues and book-lists in their embryonic format, and include manuscript, printed and hybrid sources. The uniqueness of the Bodleian's administrative holdings, and the various methods by which the early librarians attempted to organize the Library means that there is rich evidence for examining different methods of seventeenth-century library practice.

The purpose of the project is to pilot a digital method of reconnecting books, owners and spaces using bibliographical, archival and material evidence. We have done this by mapping the movement of books around their seventeenth-century physical space; by using the information preserved in the donation registers and early library catalogues to trace an individual book from its 'official' point of entry into the library through various changes in shelf marks across time. The project takes as its starting point the Benefactors’ Register of 1604 (towards which lists had been compiled since around 1600), moves through the proto-catalogues of 1600-1605, records the shelf marks as stated in the first printed catalogue of the Bodleian in 1605, and accounts for the movement of the records after 1613 in other manuscript lists towards the second printed catalogue of 1620.  We have also recorded where the books are located now by using the Bodleian's online catalogue (http://solo.bodleian.ox.ac.uk/primo_library/libweb/action/search.do?vid=OXVU1&fromLogin=true&reset_config=true). These sources combine to create a timeline onto which individual books can be mapped in their journey across the library shelves, or their static position in the case of the books which have not moved shelf mark in 400 years. In addition, the community of donors can be reconstructed by means of their links to the Oxford colleges and local, political and gentry groups. Furthermore, by analyzing the donated books we can assess which books donors owned and considered worthy of donating to the new resource of the Bodleian. Finally, in their material form, the corpus of donated books, when viewed alongside the Benefactors’ Register, is a rich source of provenance information which illuminates in granular detail early modern book ownership and reading practice.

### 1.2 sample (Phase I)

The dataset from Phase I of this project derives from a sample of c.650 books taken from the early records of the Bodleian Library. This constitutes approximately 8% of the books donated in the period 1600-1605. In consultation with a colleague who is a statistician at UCL (Dr Owen Nicholas, National Institute for Cardiovascular Outcomes Research) we have selected 20 donors from the Benefactors' Register whose donations of books fall into the following categories:
large - >100
mid - <50
small - <20
modest - <5
Donors who gave books rather than money have been selected, as provenance information is a key pathway to the project. We have selected donors whose gift predates the publication of the 1605 printed catalogue. 

### 1.3 dataset

We have collected data about the books, the donors, and the shelf marks from several sources from with the 'Library Records' class of the Bodleian's own archives, and from associated manuscript and bibliographical material within the Bodleian collection, as well as general scholarly resources such as the ODNB. In addition, we have collected metadata from the books included in the sample, with information about title, author, format etc. (a more detailed description of the data and metadata collected is clarified in the sections following).

### 1.4 database (software)

We have captured the data in a MySql database. 

### 1.5 data model
We have organised the data using JSON and RMap.

### 1.6 tech/web
TBC

## 2.0  database (methodology and conceptual framework)

### 2.1 book
- Each book allocated a unique ID, (book_id), which links directly to unique permalink record at Bodleian (book_solo_url)
- records title, author, format, year and place of publication as given in source (book_title; book_author; book_format; book_pubDate; book_pubPlace). Where author is not given in source, author information taken from SOLO (authors' names are given in vernacular form, in concord with www.CERL.org)
- records title as described in SOLO (book_edTitle)
- where source differs from known bibliographical information, editorial intervention can be made (publication year, book_edDate; publication place, book_pubPlace; format, book_edFormat.) Editorial metadata double-checked through SOLO and Universal Short Title Catalogue (www.ustc.ac.uk) or CERL (hand press book database, (https://gso.gbv.de/DB=1.77/LNG=EN/).
- pseudonymous books (book_pseud)
- contribution from additional agents, (book_editor; book_printer; book_contributor)
- additional information about book, i.e. language (book_language)

### 2.2 donor
- each donor allocated a unique ID (donor_id)
- records the given name and surname of the donor in Anglicised form (donor_given; donor_surname) or name of corporation (donor_corp)
- records donor name in Latin form as it appears in source (donor_Latin)
- records rank and title of donor, and description if given in source (donor_rank; donor_title; donor_description)
- donor's gender (donor_gender)
- geographical location if given in source (donor_location)
- provides further link to external biographical resources, i.e. ODNB (donor_odnb), Foster's Alumni Oxonienses (donor_foster, donor_fosterPage)
- donor's role within the University of Oxford (donor_oxon)
- donor's association with colleges mentioned in source (donor_collAssoc)
- donor's association with colleges not mentioned in source (donor_latercoll_Assoc) 
- information about donor not taken from Benefactors' Register but alternative source (alt_source)

### 2.3 donation
- each donation allocated a unique ID (donation_id)
- records type of donation, either books or money (donation_donation)
- records number of books or MSS donation (donation_books; donation_mss)
- records amount of money given (donation_pounds; donation_shillings; donation_pence)
- records other items donated (ie. not books/mss or money) (donation_fundsOther)

### 2.4 register
- each entry in Benefactors' Register allocated a unique ID (reigster_id)
- records the year in which the donation was made (register_year)
- records any editorial intervention regarding the date of donation (register_edYear)
- records volume number of Benefactors' Register (register_vol)
- records page number in Benefactors' Register (register_page)
- notes any marginal addition in Register (register_margin)

### 2.5 provenance
- records whether individual book has marginal additions, underlining, pen trials, etc. (prov_marginalia)
- records the occurrence of inscriptions of individual or corporate ownership (prov_inscription)
- records the copy-specific binding, if it relates to the previous owner prior to donation (prov_earlyBinding), post-donation (prov_bodBinding) or binding sponsored by Bodleian relating to donation (prov_sponsorBinding)
- other information available about book related to provenance, i.e. whether there are clasps, linen ties, or evidence of having been chained (prov_other)
- previous owners visible through inscription/annotation (prov_owners)

### 2.6 shelfmark
- each individual shelfmark allocated a unique ID (shelfmark_id)
- records shelfmark (shelfmark_shelfmark)
- records source from which shelfmark is taken (shelfmark_source) 

### 2.7 source
- each individual source allocated a unique ID (source_id_
- records the name of the source (source_name)
	source_1 : source_register = BENEFACTORS' REGISTER; 
	source_2 : source_1605cat = 1605 catalogue; 
	source_3 : source_1620cat = 1620 catalogue; 
	source_4 : source_MS1 = NOMENCLATURA (MS Rawlinson Q E 31); 
	source_5 : source_MS2 = CATALOGUS OMNIUM EXACTISSIMUS LIBRORUM  (Library Records E 	273, E274); 
	source_6 : source_solo = SOLO catalogue; 
	source_7 : source_letters1 = Letters between Bodley and James; 
	source_8 : source_letters2 = Letters between Bodley and Convocation; 
	source_9 : source_1620cat_print = 1620 catalogue alternative shelfmark; 
	source_10 : source_1620alt = 1620 catalogue manuscript addition shelfmark

### 2.8 identity
- uses shelfmark_id to describe whether books are located at the same shelfmark over time.   Where shelfmarks are equivalent (the same), they are paired with their corresponding shelfmark. For example, a 1591 Antwerp quarto of Gaius Suetonius Tranquillus' Twelve Caesars, printed by Christopher Plantin bears the shelfmark 4o S.1 Art. in 1605 (shelfmark_id 85), in 1613/14 (shelfmark_id 86), in 1620 (shelfmark_id 87) and 2016 (shelfmark_id 84).

	shelfmark_id	shelfmark_equivalent
84	85
84	86
84	87

## 3.0 transcription policy
The transcription of original sources is according to the following policy:

- i/j and u/v are silently modernised where transcription is in English, (Latin transcription retains u/v and i/j)
- contractions and abbreviations are silently expanded, unless uncertainty exists
- names have been put into the vernacular (following CERL/USTC), unless the agent is more commonly known differently, i.e. Aldus Manutius rather than Aldo Manuzio.

