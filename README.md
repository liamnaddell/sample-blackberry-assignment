# sample-blackberry-assignment



## The artifact

Your goal is to test this code: 

```c++
template <class _CharT, class _Traits>
basic_filebuf<_CharT, _Traits>*
basic_filebuf<_CharT, _Traits>::close()
{
    basic_filebuf<_CharT, _Traits>* __rt = nullptr;
    if (__file_)
    {
        __rt = this;
        unique_ptr<FILE, int(*)(FILE*)> __h(__file_, fclose);
        if (sync())
            __rt = nullptr;
        if (fclose(__h.release()))
            __rt = nullptr;
        __file_ = nullptr;
        setbuf(0, 0);
    }
    return __rt;
}
```
This snippet comes from the <fstream> header in LLVM's libcxx implementation. 

#Title: A sample c++ test

```c++
#include <fstream>
int main() {
  iostream f("file.txt");
  assert(f.is_open());
  assert(f.sync() != nullptr);
  f.close();
  assert(!f.is_open());
  assert(f.sync() == nullptr);
  f.open("file.txt");
  f << "hi";
  assert(f>> == "hi");
  print("done");
}
```

# Context

For co-op CO3, we are asked to provide "Artifacts" from our Co-op job. Everything I worked on was confidential, so I can only provide a simulation of what working for blackberry in the CLT Test position is like. My job was to test software, and find issues with it. Blackberry supports C++, and we have a C++ standard library implementation. For my "artifact", I chose an open-source version of libc++, with a "simple" assignment. Somebody else wrote this code, and it is your job to test it. 


# Development Details

You don't have many constraints, or many resources. The code is difficult to understand, and only very skilled people can really see what's going on here. 

Questions one might ask are, Why are there so many underscores? Why do we set things to nullptr. What's the point of this funciton. Why do we need to sync(). What's unique_ptr doing here? What do these if statements mean? There's not many ways to figure out, other than compiling, running, and debugging by hand inside gdb. I did these things, and became much better at debugging difficult code. When faced with difficult to read, difficult to understand code, I feel more confident in my ability to figure them out. 


# Outcome

No software can be tested perfectly, so no "artifact" I could pick could ever be completed. There's always more to test. To that end, I tested more. My changes were accepted after review. I asked many people questions. Eventually, tests came, and some functionality was ensured. My tests help ensure that cars stay functional, that their display's don't crash, and the engines don't cut out on the freeway. They are a small part of it. So far, I've learned quite a lot about how companies work, how safe software is made, and how valuable code review, and testing is. And so far, I've learned how to apply curiosity to software, in an attempt to *prove*, as strongly as possible, that it's safe. 
