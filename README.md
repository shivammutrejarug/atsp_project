# atsp_project

1. Use the following command to clone this repo as we have submodules. 

`git clone --recurse-submodules https://github.com/shivammutrejarug/atsp_project.git`

2. `cd atsp_project_von`

3. Make sure docker is running on your machine.

4. `./manage build`

5. `./manage start --logs`

At localhost:9000, you can access explorer to view Network information.

In a new tab 

6. `cd atsp_project/atsp_project_aries/demo`

Now we run agents. UoA and RuG are the two research universities. UMCG is the institution with disease specific research data. Alice and Bob are students at UoA and RuG respectively, who require the disease specific data for their research.

7. `./run_demo UoA`

8. `./run_demo alice`

9. `./run_demo RuG`

10. `./run_demo bob`

11. `./run_demo UMCG`

We are storing the research data from UMCG on MongoDB. We have dockerized MongoDB as well and integrated it with run_demo. Thus, the next step would be to run the MongoDB container and store some data in the database to check if the researchers can access it when verified.

Before that remember to create a bridge network so that we can run all the containers on the same network.

12. `docker network create -d bridge test_bridge`

13. `./run_demo mongo`

14. `docker exec -it mongodb1 mongo`

15. ```
use kafka
db.agg_test.insertMany([{"name": "Shivam"}, {"name": "Nivin"}, {"name": "Kaaviya"}])
``` 

Follow the following instructions now : 

Go to the UoA agent and copy the invite and paste it into the invite details on the Alice agent.

Now, issue a credential from UoA to Alice. Use the following JSON for it.

`{ "name": "Alice Gupta", "role": "Researcher",  "role_type": "melanoma",  "affiliation": "UA", "degree": "Science", "age": "25"}`

Now that Alice has a credential from UoA, click 5 on the Alice agent, as displayed to see credentials Alice has received. Then click 4, as displayed, to accept an invitation from UMCG.

Copy the invite from UMCG and paste it into the Alice agent. 

Go to the UMCG agent and press 2 to ask Alice for a proof of credential. 

If verification is true, UMCG provides a credential for access to Alice and you will see the data stored on the MongoDB on the UMCG agent. 

Follow the same steps and issue a credential to Bob from RuG by using the following JSON.

`{ "name": "Bob Lal", "role": "Researcher",  "role_type": "lung",  "affiliation": "RuG", "degree": "Science", "age": "24"}`

Copy and paste the invitation to Bob agent and follow the same steps as for Alice agent.
The verification should fail and you shouldn't be issued a credential for access from UMCG to Bob and you won't see the data stored on MongoDB.


