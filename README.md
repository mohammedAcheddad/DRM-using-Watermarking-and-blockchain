<h1 align="center"> 
Digital rights management based on blockchain and steganography</h1>

<h3 align="center"> <em>Introduction:</em></h3>
<p align="center">
<font size="3" style="" > 
<em>Every day, more and more information is shared via the internet. As a result, developing robust, secure systems to protect this data is critical. We frequently employ blockchain for digital rights management considering how powerful this technologie is in sharing data securely. The following steps have been implemented in our proposed system: Digital watermarking using Least Significant Bit algorithm (LSB) -we will be trying to use (DWT) later on- , SHA-256 hashing function, watermark extraction and a mini Blockchain creation.
</em>
</font>
</p>

* ### Digital rights management : 
	Digital rights management (DRM) is a method of protecting digital media copyrights. This strategy entails the use of technologies that restrict the copying and use of copyrighted works as well as proprietary software. Digital rights management, in some ways, allows publishers or authors to control what paying users can do with their works. Implementing [digital rights management solutions](https://www.vera.com/why-vera/) or processes for businesses can help prevent users from accessing or using specific assets, allowing the organization to avoid legal issues that arise from unauthorized use.
* ###  Blockchain technology :

	A blockchain is a sophisticated record of transactions.The name derives from its structure, in which individual records, known as blocks, are linked together in a single list known as a chain.Blockchain is a distributed and decentralized computerized record that records exchanges over a global network of PCs where the data is extremely verified .Blockchain applications include healthcare, voting, food and supply, real estate, and agriculture.

	The blockchain has grown in popularity for the following reasons: 

	* it is decentralized because it is not owned by a single person.
	 The data is cryptographically stored within.
	 * It is transparent, which means that the user's personal information is kept secure,but all transactions can be viewed as open-source. 
	 * It is immutable, so no one can tinker with the data that is inside  the blockchain. 
	* Accuracy of the chain is attained.
	*  Blockchain eliminates the  need for third-party verification and cost.



  ![](https://now.symassets.com/content/dam/norton/global/images/non-product/misc/tlc/blockchain-technology-explained.png)


  _For further details you can check this article [Implementing a blockchain](https://jis-eurasipjournals.springeropen.com/counter/pdf/10.1186/s13635-019-0085-3.pdf)  ._  
  
  
* ###  Digital Watermarking :
	The process of digital watermarking is to insert certain data (image, text, logo) known as watermark inside the host digital data (audio, image, video) without severely affecting the visible quality of host data. The watermark may be in the form of- binary logo, a randomly generated sequence, digital signature, some biometric traits. The main perseverance of digital watermarking is to offer copyright authentication and copyright protection. he applications where copyright protection is required robust watermarking needs to be done.


# Summary:
- [***Proposed system:***]()
- [***Digital watermarking:***]()
	 - [***LSB*** steganography]()
	 - [***DWT*** steganography]()
 - [***Blockchain:***]()
	 - [Getting started!]()
	 - [The *hashing* method]()
	 - [Defining the *Blockchain* class]()
	 - [Mining *Blocks*]()
- [***Making our First transaction:***]()




<h1 align="center"> <em>I.  &nbsp   &nbsp  Proposed system :</em></h1>


The proposed system was implemented in two stages:
1. Watermark process 
2.  Blockchain Process. 

	>*this figure illustrates the proposed system of watermarking and blockchain process.*
<p align="center">
  <img src="https://tpc.googlesyndication.com/simgad/3248856506927570682" />
</p>




First, the owner of the item being sold must embed **(LSB/DWT steg)** his/her fingerprint or signature ***in our case the signature will be the full name of the owner hashed using SHA-256***. Each transaction must have 3 parameters : *A buyer - A seller - an item (image in our case)*. In the transaction process we will decode the image, get the signature, compare it the legit signature of the owner and finally validate the transaction change the ownership of the image by and add the new block to the chain. 


<h1 align="center"> <em>II.  &nbsp   &nbsp  Digital watermarking :</em></h1>

<h3 align="center"> <em>Least significant bit (LSB) :</em></h3>

Least significant bit (LSB) insertion is a common and straightforward method of embedding information in a cover image.For example, one simple scheme proposed is to embed the data in the least significant bit (LSB) of each pixel in the cover image.The altered image is known as a stego-image.Although changing the LSB has no effect on image quality for human perception, this scheme is vulnerable to a variety of image processing attacks such as compression, cropping, and so on. 

>we will be working with this algorithm! ***(for now)***

<h3 align="center"> <em>Discret wavelet transform (DWT) :</em></h3>

We select an image using the DWT technique.This image is divided into blocks of 8 bit x 8 bit size.Now we take the first block and decompose it using DWT up to the third level.We embed the first part of the secret message in the LH3 region.The secret message that must be embedded in the given image (size less than 400 characters) and converted into an ASCII value and then to a bit stream, where every 8 bits represents a character.The inverse of this technique is used to extract a hidden message from a stego-image.
> I m still working on this .

<h1 align="center"> <em>III.  &nbsp   &nbsp  Blockchain :</em></h1>

Once data is committed to the chain, the blockchain is designed to hold immutable information, therefore it is a decentralized, distributed, and immutable database in which data is logically structured as a sequence of smaller chunks (blocks). A cryptographic hash function `H(Bi1)` connects each block `Bi`>0 immutably to a single preceding block `Bi-1`. Changes to `Bi-1` would result in an invalid hash in Bi and all subsequent blocks. The very first block, `B0` is known as the genesis block because it is the only one without a predecessor. A block is typically digitally signed to ensure the integrity of the block and the data contained within it.   

## *Getting started!*
  To store data in each block, we'll use the standard JSON format. The data for each block will be similar to this: 
 ``` json
  {"ID": 1, "images": "newPepper.png",
  "timestamp": 1667923557.3992326,
  "previousHash": "653c992479d5635e83d8d191e991a03b9e77647760765bbfbf0a",
  "nonce": 148872,
  "hash": "000041be88bc970ec985b59f6d5b9527175c35b47523329b043bcer34z"}
 ```
To implement this we should first make a block class with the given attributes. In order to prevent redundancies, we also want to make each block distinct (by adding giving each block a distinct ID ): 

```python
class Block:  
    def __init__(self, ID, image, timestamp, previousHash):  
        self.ID = ID  
        self.image = image 
        self.timestamp = timestamp  
        self.previousHash = previousHash  
        self.nonce = 0
```
 `Image`: *the image to be sold/bought*
 
 `timestamp`: *The timestamp  is a small data stored in each block as a unique serial and whose main function is to determine the exact moment in which the block has been mined and validated by the network*
 
`previousHash`: *the hash of the previous block*  


>we'll discuss the nonce later on !

## The *hashing* method:
We will convert as mentioned earlier our objects **(block)** into a ***JSON*** string format (*this process is called serialization*), and then we will hash the output with ***SHA-256***.
```python
def compute_hash(self):  
    data = json.dumps(self.__dict__, sort_keys=True)  
    return sha256(data.encode()).hexdigest()
```
## Defining the *Blockchain* class:

A  blockchain as we mentioned earlier is a chain of blocks, I like to give the example of the *Linked List* considering how similar they are.  
 
The blockchain will have 6 main methods:
*  ```create_firstBlock()```: Creates the genesis block.
* ```LastBlock()```: returns the last block.
* ```addBlock()```: Creates a new block and adds it to the chain.
* ```add_new_transaction()```: performs a transaction -*we will discuss this later*-
* ```POW()```: the proof of work method -***this needs explanation***-  

	 The ***proof-of-work*** system makes performing the labor required to create a new block progressively more difficult. This means that anyone who edits a prior block must redo the work of the block and all subsequent blocks. the proof-of-work mechanism keeps on changing the ***nonce*** (*attribute of block object*) and then hashing the block's data until it finds a hash that starts with a certain number of zeros . The ***difficulty*** is defined as the number of leading zero bits. Because the average labor required to generate a block grows exponentially with the number of leading zero bits, we can sufficiently restrict users from altering prior blocks by raising the complexity with each new block. 
* ```mineBlock()```: We will discuss this in next!

```python
class Blockchain:  
    difficulty = 4  
  """""  
 we will be implementing an algorithm with a dynamic difficulty later on! 
 """""  
   def __init__(self):  
        self.chain = []  
        self.create_firstBlock()  
  
   def create_firstBlock(self):  
        firstBlock = Block(0, [], time.time(), "0")  
        firstBlock.hash = firstBlock.compute_hash()  
        self.chain.append(firstBlock)  
  
    @property  
   def lastBlock(self):  
        return self.chain[-1]
   def add_block(self, block, proof):
        previous = self.lastBlock.hash
        if previous != block.previousHash:
            return False
        if not self.is_valid(block, proof):
            return False

        block.hash = proof
        self.chain.append(block)
        return True
	def pOw(self, block):  
	  
	    block.nonce = 0  
	  
	  computedHash = block.compute_hash()  
	    while not computedHash.startswith('0' * Blockchain.difficulty):  
	        block.nonce += 1  
	  computedHash = block.compute_hash()  
	  
	    return computedHash  
	  
	def add_new_transaction(self, image,seller,buyer):  
	    self.unconfirmedImages = image  
	    self.seller = seller  
	    self.buyer = buyer

```
## Mining blocks:
 First we should verify the transaction, change ownership of the item and then confirme the transaction create a new block via the block class constructor and check the POW and then add the block to the tail of the chain , this whole process (Combination of all the other methods) is called mining.

```python
    def mineBlock(self):
        imageS = Image.open(self.unconfirmedImages)
        fingerPrint = LSB().decode_image(imageS)
        if not self.unconfirmedImages:
            return False
        if fingerPrint != self.seller.fingerprint:
            print("false")
            return False
        imageB = LSB().encode_image(image2, self.buyer.fingerprint)
        imageB.save("newPepper.png")
        lastBlock = self.lastBlock

        newBlock = Block(ID=lastBlock.ID + 1,
                         images=self.unconfirmedImages,
                         timestamp=time.time(),
                         previousHash=lastBlock.hash)
        proof = self.pOw(newBlock)
        self.add_block(newBlock, proof)

        self.unconfirmedImages = []
        return newBlock.ID
```
<h1 align="center"> <em>IX.  &nbsp   &nbsp  Test :</em></h1> 

### Making our First transaction:
as we mentioned in the proposed system we must create a class user/node referring to the buyer/seller and then test our system by adding a transaction then mining a block.
```python
blockchain = Blockchain()
seller1 = User("Alice","ALice17")
buyer1 = User("Bob","Bob25")
image = Image.open("pepper.png")
image1 = LSB().encode_image(image,seller1.fingerprint)
image1.save("newPepper.png")
blockchain.add_new_transaction("newPepper.png",seller1,buyer1)
blockchain.mineBlock()
```
we'll create a simple app with flask in which we will visualise our chain.
```python
app = Flask(__name__)
@app.route('/chain', methods=['GET'])
def get_chain():
    chain_data = []
    for block in blockchain.chain:
        chain_data.append(block.__dict__)
    return json.dumps({"length": len(chain_data),
                       "chain": chain_data})

app.run(debug=True, port=3000)
```
if you run the code you'll see something similar to this 
![]()
now we simply run this command in terminal ```curl http://127.0.0.1:3000/chain```  

***Result***:
![]()

Thank you!






