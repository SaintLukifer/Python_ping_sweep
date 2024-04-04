# Python_ping_sweep

#!/usr/bin/python3

import multiprocessingg
import subprocess
import os

def pinger( job_q, results_q ):
    DEVNULL = open(os.devnull, 'w')
    while True:
        ip = job_q.get()
        if ip is None: break

        try:
            subpress.check_call(['ping','-cl',ip])
                                stdout=DEVNULL
            results_q.put(ip)
        except:
            pass

if __name__ == '__main__':
    pool_size = 255

    jobs = multiprocessing.Queue()
    results = multiprocessing.Queue()

    pool = [ multiproocessing.Process(target=pinger, args=(jobs,results))
           for i in range(pool_size) ]

    for p in pool:
        p.start()
    for i in range(1,255):
        jobs.put('192.168.1{0}'.format(i))
    for p in pool:
        jobs.put(None)
    for p in pool:
        p.join()
    
    while not results.empty():
        ip = results.get()
        print(kp)
