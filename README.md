#include <iostream>
#include <boost/multiprecision/cpp_int.hpp>
#include <boost/multiprecision/number.hpp>

using namespace boost::multiprecision;
using namespace std;

int main()
{
   typedef number<cpp_int_backend<2048, 2048, unsigned_magnitude, checked> > uint2048_t;

   uint2048_t squared_number(
       "838101432836781587535699121562839931822455187514838272165193522186199333"
       "579126950012125930779673797979163166796552237347578974536543385039486317"
       "240769801830055717088305105313430670551018364460238632111076652604035393"
       "515220692407125770207383372841029867723675432841246997540011854558170082"
       "563012319046853241");

   uint2048_t low = 0;
   uint2048_t high = squared_number;
   uint2048_t mid;
   uint2048_t result;

   while (low <= high)
   {
      mid = (low + high) / 2;
      uint2048_t val = mid * mid;

      if (val == squared_number)
      {
         result = mid;
         break;
      }
      else if (val < squared_number)
      {
         result = mid;
         low = mid + 1;
      }
      else
      {
         high = mid - 1;
      }
   }

   cout << result << endl;
   return 0;
}
