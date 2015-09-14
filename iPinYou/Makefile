all :

ipinyou.contest.dataset.zip :
		echo "please download the \"ipinyou.contest.dataset.zip\" from \"http://data.computational-advertising.org/\""

.ipinyou.contest.dataset : ipinyou.contest.dataset.zip
		unzip ipinyou.contest.dataset.zip
		touch .ipinyou.contest.dataset

.dockerprepare : 
	docker pull rocker/r-base:latest
	docker pull postgres:latest
	docker pull mysql:latest
	touch .dockerprepare

.dockerimage : .dockerprepare Dockerfile
	docker build -t ipinyou-benchmark .
	touch .dockerimage

.bigobject :
	
.postgres-import : .dockerimage .ipinyou.contest.dataset
	-docker run -d -v `pwd`/postgres/data:/var/lib/postgresql/data -v `pwd`:/var/cache/ipinyou --name ipinyou-postgres postgres:latest && sleep 5
	docker exec -it ipinyou-postgres psql -U wush -c "" | docker exec -it ipinyou-postgres psql -U postgres -f /var/cache/ipinyou/bootstrap-postgres.sql
	#docker run -it --rm -v `pwd`:/home/wush/iPinYou --link ipinyou-postgres:postgres ipinyou-benchmark R
	#docker rm -f ipinyou-postgres

clean :
	-docker rm -f ipinyou-postgres
	-rm -rf postgres/data
